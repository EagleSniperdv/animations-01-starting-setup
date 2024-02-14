<template>
  <router-view v-slot="slotProps">
    <transition name="route" mode="out-in">
      <component :is="slotProps.Component"></component>
    </transition>
  </router-view>
</template>  

<script>

export default {
  components: {
  
  },
  data() {
    return { 
      animatedBlock: false,
      dialogIsVisible: false ,
      ParIsVisible: true,
      enterInterval: null,
      leaveInterval: null

    };
  },
  methods: {
    enterCancelled() {
      clearInterval(this.enterInterval);
    },

    leaveCancelled() {
      clearInterval(this.leaveInterval);
    },
    beforeEnter(el) {
      el.style.opacity = 0;
    },
    enter(el,done) {
      let round = 1;
      this.enterInterval = setInterval(() => {
        el.style.opacity = round * 0.01;
        round++;
        if (round > 100)  {
          clearInterval(this.enterInterval);
          done();
        }
      },20);
    },
    beforeLeave(el) {
      el.style.opacity = 1;
    },
    leave(el,done) {
      let round = 10;
      this.leaveInterval= setInterval(() => {
        el.style.opacity = 1 - round * 0.01;
        round++;
        if(round > 100) {
          clearInterval(this.leaveInterval);
          done();
        }
      },20);
    },

    onAfterEnter() {

    },

    togglePar() {
      this.ParIsVisible = !this.ParIsVisible;
    },
    transformBox() {
      this.animatedBlock = true;
    },
    showDialog() {
      this.dialogIsVisible = true;
    },
    hideDialog() {
      this.dialogIsVisible = false;
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  font-family: sans-serif;
}
body {
  margin: 0;
}
button {
  font: inherit;
  padding: 0.5rem 2rem;
  border: 1px solid #810032;
  border-radius: 30px;
  background-color: #810032;
  color: white;
  cursor: pointer;
}
button:hover,
button:active {
  background-color: #a80b48;
  border-color: #a80b48;
}
.block {
  width: 8rem;
  height: 8rem;
  background-color: #290033;
  margin-bottom: 2rem;

  /* transition: transform 0.3s ease-out; */
}
.container {
  max-width: 40rem;
  margin: 2rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 2rem;
  border: 2px solid #ccc;
  border-radius: 12px;
}

.animate {
  animation: slide-fade 0.3s ease-out forwards;
  /* transform: translateX(-50px); */
}

.route-enter-from {

}

.route-enter-active{
  animation: slide-fade 0.4s ease-out;
}

.route-enter-to {

}

.route-leave-active {
  animation: slide-fade 0.4s ease-out;
}


@keyframes slide-fade {
  0% {
    transform: translateX(0) scale(1.1);
  }

  

  100% {
    transform: translateX(-40px) scale(1);
  }
}
</style>