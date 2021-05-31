<template>
	<div class="dashboard">
		<header>
			<img src="@/assets/imgs/LOGO.svg" alt="logo" />
		</header>
		<main>
			<div class="headOfTableMob">
				<h4>Панель котировок</h4>
			</div>
			<div class="tableContainer">
				<div class="headOfTable">
					<h1>Панель котировок</h1>
				</div>
				<div class="table">
					<table>
						<thead>
							<tr>
								<td><h3>Валютные пары</h3></td>
								<td><h3>Изменение</h3></td>
								<td><h3>Цена</h3></td>
							</tr>
						</thead>
						<tbody>
							<tr
								v-for="pair in currencyPairs"
								:key="pair.id"
								v-bind:class="{ active: pair.isActive }"
								v-on:click="selectPair(pair)"
							>
								<td>
									<h2>{{ pair.value[0] }} | {{ pair.value[1] }}</h2>
								</td>
								<td>
									<h2><img :src="pair.imgSrc" /> {{ pair.changedPercentPerDay }}</h2>
								</td>
								<td>
									<h2>{{ pair.price }}</h2>
								</td>
							</tr>
						</tbody>
					</table>
				</div>
			</div>
			<div class="graphContainer">grap</div>
		</main>
	</div>
</template>

<script>
export default {
	name: "Dashboard",

	data: function () {
		return {
			connection: null,
			apiKey: "1fc9ac8cdde28a178bef9610e65668c7cb135e4da5ef3326f203b3cfdd963aae",
			timer: "",
			activePairId: 0,
			currencyPairs: [
				{
					id: 0,
					value: ["USD", "BTC"],
					price: 0,
					changedPercentPerDay: 0,
					imgSrc: "",
					isActive: false,
				},
				{
					id: 1,
					value: ["USD", "BCH"],
					price: 0,
					changedPercentPerDay: 0,
					imgSrc: "",
					isActive: false,
				},
				{
					id: 2,
					value: ["USD", "ETH"],
					price: 0,
					changedPercentPerDay: 0,
					imgSrc: "",
					isActive: false,
				},
				{
					id: 3,
					value: ["USD", "XRP"],
					price: 0,
					changedPercentPerDay: 0,
					imgSrc: "",
					isActive: false,
				},
			],
		}
	},
	methods: {
		sendMessage: function (subRequest) {
			let self = this
			self.connection.send(JSON.stringify(subRequest))
		},
		cancelAutoUpdate() {
			clearInterval(this.timer)
		},
		currencyPairsImgChanger: function (pair) {
			if (pair.changedPercentPerDay > 0) {
				pair.imgSrc = require("../assets/imgs/arrow_up.svg")
			} else if (pair.changedPercentPerDay == 0) {
				pair.imgSrc = ""
			} else {
				pair.imgSrc = require("../assets/imgs/arrow_down.svg")
			}
		},
		selectPair: function (pair) {
			this.currencyPairs[this.activePairId].isActive = false
			this.activePairId = pair.id
			pair.isActive = true
		},
	},
	/* created: function () {
		let self = this
		this.connection = new WebSocket("wss://streamer.cryptocompare.com/v2?api_key=" + this.apiKey)
		this.connection.onopen = function onStreamOpen() {
			let subRequest = {
				action: "SubAdd",
				subs: [
					"0~Coinbase~BTC~USD",
					"0~Coinbase~BCH~USD",
					"0~Coinbase~ETH~USD",
					"0~Coinbase~XRP~USD",
					"24~CCCAGG~BTC~USD~D",
					"24~CCCAGG~BCH~USD~D",
					"24~CCCAGG~ETH~USD~D",
					"24~CCCAGG~XRP~USD~D",
				],
			}

			this.timer = setInterval(() => self.sendMessage(subRequest), 1000)
		}

		this.connection.onmessage = function onStreamMessage(event) {
			let message = JSON.parse(event.data)
			let id = 0

			if (message.TYPE == 0) {
				switch (message.FSYM) {
					case "BTC":
						id = 0
						break
					case "BCH":
						id = 1
						break
					case "ETH":
						id = 2
						break
					case "XRP":
						id = 3
						break
				}
				self.currencyPairs[id].price = message.P
			}
			if (message.TYPE == 24) {
				switch (message.FROMSYMBOL) {
					case "BTC":
						id = 0
						break
					case "BCH":
						id = 1
						break
					case "ETH":
						id = 2
						break
					case "XRP":
						id = 3
						break
				}
				self.currencyPairs[id].changedPercentPerDay = (
					((message.OPEN - message.CLOSE) / ((message.OPEN + message.CLOSE) / 2)) *
					100
				).toFixed(2)
				self.currencyPairsImgChanger(self.currencyPairs[id])
			}
		}
	}, */
	beforeDestroy: function () {
		this.cancelAutoUpdate()
	},
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.dashboard {
	display: flex;
	flex-direction: column;
	height: 100vh;
	header {
		position: fixed;
		width: 100%;
		height: 60px;
		left: 0px;
		top: 0px;
		display: flex;
		align-items: center;
		justify-content: center;

		/* Dark Gray */

		background: #191a20;

		img {
			margin: 0;
		}
	}
	main {
		margin-top: 60px;
		flex: 1;
		display: flex;
		.headOfTableMob {
			display: none;
		}
		.tableContainer {
			flex: 27;
			background-color: #191a20;

			.headOfTable h1 {
				font-family: "Montserrat";
				font-style: normal;
				font-weight: 600;
				font-size: 24px;
				text-transform: uppercase;
				color: #ffffff;
				padding: 22px 35px;
			}
			.table table {
				width: 100%;
				box-sizing: border-box;
				table-layout: fixed;
				white-space: nowrap;
				border: none;
				border-spacing: 0;

				thead tr td h3 {
					font-family: "Montserrat";
					font-style: normal;
					font-weight: 400;
					font-size: 16px;
					line-height: 150%;
					color: #757679;
				}
				tbody tr {
					cursor: pointer;
					td h2 {
						font-family: "Montserrat";
						font-style: normal;
						font-weight: 600;
						font-size: 20px;
						line-height: 150%;
						text-transform: uppercase;
						color: #ffffff;
					}
				}

				.active {
					background: linear-gradient(90deg, rgba(31, 70, 106, 0.88) 0%, #191a20 138.3%), #191a20;
					border-radius: 0.5px;
				}

				tr td:first-child {
					padding-left: 35px;
				}

				tr td:nth-child(2) {
					text-align: center;
				}

				tr td:last-child {
					text-align: right;
					padding-right: 35px;
				}
			}
		}
		.graphContainer {
			flex: 73;
			background-color: #eeeeee;
		}
	}

	@media screen and (max-width: 640px) {
		header {
			height: 30px;
			img {
				width: 64px;
				height: 11px;
			}
		}
		main {
			flex-direction: column;
			margin-top: 30px;
			.tableContainer {
				order: 2;
				flex: 1;
				padding: 13px 14px 0 15px;
				.table table thead tr td h3 {
					margin: 0;
					font-weight: 400;
					font-size: 12px;
				}
			}
			.graphContainer {
				order: 1;
				flex: 1;
			}
			.headOfTableMob {
				display: flex;
				order: 0;
				background-color: #191a20;
				height: 25px;
				h4 {
					margin: 0;
					font-family: "Montserrat";
					font-style: normal;
					font-weight: 600;
					font-size: 14px;
					line-height: 150%;
					color: #ffffff;
					padding: 2px 15px;
				}
			}
			.headOfTable {
				display: none;
			}
		}
	}
}
</style>
