<template>
  <div class="home">
    <Transition name="bounce">
      <img v-if="isLogoVisible" alt="Vue logo" src="../assets/logo.png" />
    </Transition>
    <button @click="handleClick" class="button">start</button>
    <transition name="appear">
      <img v-if="!isLogoVisible" alt="Vue logo" src="../assets/logo.png" />
    </transition>
    <MthsBttst3 />
  </div>
</template>

<script>
// @ is an alias to /src
import MthsBttst3 from "@/components/studies/MthsBttst3.vue";

export default {
  name: "HomeView",
  components: {
    MthsBttst3,
  },
  data: () => ({
    isLogoVisible: false,
  }),
  methods: {
    handleClick() {
      this.isLogoVisible = !this.isLogoVisible;
    },
  },
};
</script>
<style scoped>
.appear-enter-active,
.appear-leave-active {
  transition: transform 0.4s, opacity 0.4s;
}
.appear-leave-to,
.appear-enter-from {
  transform: translateY(-200%);
  opacity: 0;
  transform: scale(0);
}

.appear-leave,
.appear-enter-to {
  transform: scale(1);
  transform: translateY(200);
  opacity: 1;
}

/* modelo doc vue transition */
.bounce-enter-active {
  animation: bounce-in 0.5s;
}
.bounce-leave-active {
  animation: bounce-in 0.5s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.25);
  }
  100% {
    transform: scale(1);
  }
}

/* style bar*/
* {
  margin: 0 auto;
}
.button {
  background: #34495c;
  color: #fafafa;
  outline: 0;
  font-weight: bold;
  font-size: 2rem;
  border-radius: 1rem;
  border: none;
  padding: 0.5em 3em;
  cursor: pointer;
  display: block;
  margin-bottom: 4rem;
}
button::-moz-focus-inner {
  border: 0;
}
</style>
