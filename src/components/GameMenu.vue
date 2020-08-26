<template>
  <div class="game-menu">
    <div class="game-options">
      <h2>Уровень сложности:</h2>
      <label>
        <input type="radio" value="1500" v-model="checkbox" @change="changeCheck" />Легко
      </label>
      <label>
        <input type="radio" value="1000" v-model="checkbox" @change="changeCheck" />Нормально
      </label>
      <label>
        <input type="radio" value="400" v-model="checkbox" @change="changeCheck" />Сложно
      </label>
    </div>
    <div class="playing-menu" v-if="started"></div>
    <div class="start-menu" v-else>
      <button @click="start">Start</button>
    </div>
  </div>
</template>

<script>
import { eventEmitter } from "../main";
export default {
  name: "game-menu",
  data() {
    return {
      started: false,
      checkbox: "1500",
    };
  },
  methods: {
    start() {
      setTimeout(() => {
        this.restartGame();
      }, 500);
    },
    restartGame() {
      if (!this.$store.state.started) {
        this.started = true;
        window.$gamelights.restart();
      }
    },
    changeCheck() {
      eventEmitter.$emit("changeTrickiness", this.checkbox);
    },
  },
  mounted() {
    document.addEventListener("keyup", (e) => {
      if (e.key.toLowerCase() == "enter" || e.code.toLowerCase() == "enter") {
        this.restartGame();
      }
    });
  },
};
</script>

<style lang="sass" scoped>
.game-menu
	display: flex
	flex-direction: column
	align-items: flex-end
	background-color: #ffffff
	border-radius: 8px
	min-height: 80px
	.game-options
		display: flex
		flex-direction: column
		justify-content: flex-start
		label
			cursor: pointer
		input
			margin-bottom: 15px
	.playing-menu
		display: flex
		align-items: center
		justify-content: space-between
		padding: 8px
		height: 80px
		flex-wrap: wrap
.start-menu
	display: flex
	align-items: center
	justify-content: flex-end
	min-height: 80px
	height: 100%
	button
		background-color: #78BCFF
		border: none
		outline: none
		padding: 12px 30px
		border-radius: 5px
		margin-top: -10px
		font-size: 20px
		font-weight: 400
		cursor: pointer
		color: #000000
		transition: 200ms
		&:hover
			background-color: #6DABE8
</style>