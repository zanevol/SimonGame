<template>
  <div class="game-lights-holder">
    <slot />
  </div>
</template>

<script>
export default {
  name: "LightsHolder",
};
</script>

<style scoped lang="sass">
.game-lights-holder
	display: flex
	flex-wrap: wrap
	flex-direction: column
	align-items: center
	justify-content: center
	background: #fff
	// position: relative
	float: left
	margin-right: 3em
	width: 300px
	height: 300px
	-webkit-border-radius: 150px 150px 150px 150px
	border-radius: 150px 150px 150px 150px
	-moz-box-shadow: 2px 1px 12px #aaa
	-webkit-box-shadow: 2px 1px 12px #aaa
	-o-box-shadow: 2px 1px 12px #aaa
	box-shadow: 2px 1px 12px #aaa
	// display: flex
	// align-items: center
	// justify-content: center
	// width: 100%
	// padding: 40px
	// grid-gap: 40px
	// background-color: #ffffff
	// border-radius: 8px
</style>
