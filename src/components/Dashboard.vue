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
							<tr>
								<td><h2></h2></td>
								<td><h2></h2></td>
								<td><h2></h2></td>
							</tr>
							<tr>
								<td><h2></h2></td>
								<td><h2></h2></td>
								<td><h2></h2></td>
							</tr>
							<tr>
								<td><h2></h2></td>
								<td><h2></h2></td>
								<td><h2></h2></td>
							</tr>
							<tr>
								<td><h2></h2></td>
								<td><h2></h2></td>
								<td><h2></h2></td>
							</tr>
						</tbody>
					</table>
				</div>
			</div>
			<div class="graphContainer">graph</div>
		</main>
	</div>
</template>

<script>
export default {
	name: "Dashboard",
	props: {},
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
			padding: 22px 35px;

			.headOfTable h1 {
				font-family: "Montserrat";
				font-style: normal;
				font-weight: 600;
				font-size: 24px;
				text-transform: uppercase;
				color: #ffffff;
			}
			.table table {
				width: 100%;
				box-sizing: border-box;
				table-layout: fixed;
				white-space: nowrap;

				thead tr td h3 {
					font-family: "Montserrat";
					font-style: normal;
					font-weight: 400;
					font-size: 16px;
					line-height: 150%;
					color: #757679;
				}
				tbody tr td h2 {
					font-family: "Montserrat";
					font-style: normal;
					font-weight: 600;
					font-size: 20px;
					line-height: 150%;
					text-transform: uppercase;
					color: #ffffff;
				}
				tr td:nth-child(2) {
					text-align: center;
				}

				tr td:last-child {
					text-align: right;
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
