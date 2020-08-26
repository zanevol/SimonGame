<template>
  <div :class="`game-lights ${state}`">
    <gl-holder>
      <gl-button :shortkey="'E'" :color="'#1E90FF'" :sound="'1.mp3'" />
      <gl-button :shortkey="'I'" :color="'#FEEF33'" :sound="'2.mp3'" />
      <gl-button :shortkey="'F'" :color="'#FF5643'" :sound="'3.mp3'" />
      <gl-button :shortkey="'J'" :color="'#BEDE15'" :sound="'4.mp3'" />
    </gl-holder>
    <game-over v-if="state == 'gameover'" />
  </div>
</template>

<script>
import GameOver from "@/components/GameLights/GameOver.vue";
import GlHolder from "@/components/GameLights/Holder.vue";
import GlButton from "@/components/GameLights/Button.vue";
import GameMenu from "@/components/GameMenu.vue";
import { eventEmitter } from "../main";

export default {
  data() {
    return {
      trickiness: "1500",
    };
  },
  name: "GameLights",
  components: {
    GlHolder,
    GlButton,
    GameOver,
    GameMenu,
  },
  computed: {
    level: {
      get() {
        return this.$store.state.level;
      },
      set(value) {
        this.$store.state.level = value;
      },
    },
    currentSequence: {
      get() {
        return this.$store.state.currentSequence;
      },
      set(value) {
        this.$store.state.currentSequence = value;
      },
    },
    state: {
      get() {
        return this.$store.state.state;
      },
      set(value) {
        this.$store.state.state = value;
      },
    },
  },
  methods: {
    play(sequence = []) {
      this.setState("waiting");
      sequence.forEach((n, i) => {
        setTimeout(() => {
          document.querySelectorAll(`[data-light-button]`)[n].click();
          if (i == sequence.length - 1) {
            this.setState("listening");
          }
        }, `${this.trickiness}` * i);
      });
    },
    levelUp() {
      this.level++;
      this.currentSequence = [];
      for (let i = 0; i < this.level; i++) {
        this.currentSequence.push(this.randomNumber(0, 3));
      }
      this.play(this.currentSequence);
    },
    restart() {
      this.setState("waiting");
      this.$store.state.started = true;
      this.$store.state.hits = [];
      this.$store.state.level = 0;
      this.$store.state.elapsedTime = 0;
      this.$store.state.currentSequence = [];
      this.$store.state.sequenceListener = undefined;
      window?.$gamelights_timer?.reset();
      setTimeout(() => {
        window.$gamelights.levelUp();
      }, 500);
    },
    gameOver() {
      this.setState("gameover");
      this.$store.state.started = false;
    },
    randomNumber(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },
    setState(state) {
      this.$store.state.state = state;
    },
    getState() {
      return this.$store.state.state;
    },
    sequence() {
      return this.currentSequence;
    },
    shiftSequence() {
      return this.currentSequence.shift();
    },
  },
  mounted() {
    window.$gamelights = this;
    eventEmitter.$on("changeTrickiness", (value) => {
      this.trickiness = value;
    });
  },
};
</script>

<style scoped lang="sass">
.game-lights
	margin-bottom: 40px
	&.waiting
		pointer-events: none
</style>
