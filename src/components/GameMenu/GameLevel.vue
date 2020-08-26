<template>
  <div class="game-level">
    <h1>Раунд: {{level}}</h1>
  </div>
</template>

<script>
export default {
  name: "game-level",
  computed: {
    level() {
      return this.$store.state.level;
    },
  },
};
</script>

<style lang="sass" scoped>
.game-level h1
	color: #000
	font-size: 22px
	font-weight: 700
</style>