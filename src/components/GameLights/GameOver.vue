<template>
  <div class="game-over">
    <div class="game-over__content">
      <h4>Конец игры</h4>
      <button @click="restart">Restart</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "game-over",
  methods: {
    restart() {
      window.$gamelights.restart();
    },
  },
};
</script>

<style lang="sass" scoped>
.game-over
	position: absolute
	left: 70%
	top: 70%

	&__content
		text-align: center
		h4
			text-transform: uppercase
			color: red
			font-size: 20px
		button
			background-color: #78BCFF
			border: none
			outline: none
			padding: 12px 30px
			border-radius: 5px
			font-weight: 400
			font-size: 20px
			cursor: pointer
			color: #000000
			transition: 200ms
			&:hover
				background-color: #6DABE8
</style>