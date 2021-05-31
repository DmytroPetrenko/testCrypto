<template>
	<div id="app">
		<Dashboard />
	</div>
</template>

<script>
import Dashboard from "./components/Dashboard.vue"

export default {
	name: "App",
	components: {
		Dashboard,
	},
}
</script>

<style lang="scss">
@font-face {
	font-family: "Montserrat";
	src: local("Montserrat"), url(assets/fonts/Montserrat/Montserrat-Regular.ttf) format("truetype");
}
html,
body {
	margin: 0;
}
</style>
