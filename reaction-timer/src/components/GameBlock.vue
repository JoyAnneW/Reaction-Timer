<template>
	<!-- this div will show after the delay, at which point showBlock will switch to true. Clicking on the block stops the timer so that the final rt can be displayed-->
	<div class="block" v-if="showBlock" @click="stopTimer">Click Me!</div>
</template>

<script>
export default {
	props: ["delay"],
	data() {
		return {
			showBlock: false,
			// this will store a set interval of 10 ms.
			timer: null,
			// every 10 ms reactionTIme will increase
			reactionTIme: 0,
		};
	},
	// lifecycle hooks. this will fire when the component has been mounted to the dom. we want to start the timer when the component has been mounted and then show the block after the delay
	mounted() {
		setTimeout(() => {
			this.showBlock = true;
			this.startTimer();
		}, this.delay);
		console.log(this.delay);
	},
	// this lifecycle hook fires whenever data is updated in our component
	updated() {
		console.log(this.timer);
	},

	methods: {
		startTimer() {
			// every 10 ms this.timer will run the setinterval method which increases reaction time. the reason setinterval is stored in a variable is so we can clear it later.
			this.timer = setInterval(() => {
				this.reactionTIme += 10;
			}, 10);
		},
		stopTimer() {
			// when the interval is cleared, it will no longer run and reaction time will no longer increase. The final reaction time will be stored
			clearInterval(this.timer);
			// in order to pass data from the child back up to the parent, we can emit a custom event that we can listen for in the parent component. when you do this, you can also pass along data, in our case, the reactiontime.
			this.$emit("end", this.reactionTime);
		},
	},
};
</script>

<style>
.block {
	width: 400px;
	border-radius: 20px;
	background-color: cadetblue;
	text-align: center;
	padding: 100px 0;
	margin: 40px auto;
}
</style>
