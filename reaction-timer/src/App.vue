<template>
	<h1>Reaction Timer</h1>
	<!-- we're data binding onto the html disabled attribute. the button will be disabled once isPlaying is true -->
	<button @click="start" :disabled="isPlaying">Start Game</button>
	<!-- data binding the delay property which is a prop -->
	<GameBlock v-if="isPlaying" :delay="delay" />
</template>

<script>
import GameBlock from "./components/GameBlock.vue";
export default {
	name: "App",
	components: { GameBlock },
	data() {
		return {
			isPlaying: false,
			// the block will appear after a random amount of time on the screen. delay keeps track of this.
			delay: null,
		};
	},
	methods: {
		start() {
			// 2000 is the smallest wait time for the block. math.random will give us a random number between 0 and 1 for a maximum wait time of 7 seconds.
			this.delay = 2000 + Math.random() * 5000;
			this.isPlaying = true;
		},
	},
};
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #444;
	margin-top: 60px;
}
</style>
