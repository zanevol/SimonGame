<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style lang="sass">
*
	box-sizing: border-box
root
	--base-font: 30px

html, body
	font-family: Arial, Helvetica, sans-serif

.container
	flex-direction: column
	max-width: 600px
	width: 100%
	position: relative
	margin: 0 auto

@media screen and (max-width: 768px)
	--base-font: 20px
</style>