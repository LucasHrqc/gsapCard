<template>
  <div class="card-animation" id="card-animation">
    <div class="img"></div>
    <p class="card-header">
      SAVAGE
    </p>
    <div class="card-text-below">
      <p>
        Lorem Lucas Henrique da Costa
      </p>
    </div>
    <div class="card-side">
      <h2>Lucas <br> Henrique</h2>
      <div class="card-on" @click="cardOn">
        <span id="card-plus">+</span>
        <span id="card-minus">-</span>
      </div>
    </div>
    <div class="card-side-text">
      <p class="card-paragraph">
        Lorem texto bem longo aqui pra mostrar como que as coisas são.
      </p>
    </div>
  </div>
</template>

<script>

import {gsap} from "gsap";

export default {
  name: "CardComponent",
  components: {},
  data() {
    return {
      timeline: null,
      card: null,
    }
  },
  mounted() {
    this.initGsap();
  },
  methods: {
    cardOn() {
      this.cardClick();
    },

    initGsap() {
      const tl = gsap.timeline();
      tl.from(".img", {
        delay: 0.5,
        y: -100,
        height: 0,
        duration: 1,
        ease: "Power2.easeInOut",
      });
      tl.from(
          ".card-side, .card-header, .card-text-below",
          {
            y: -50,
            opacity: 0,
            stagger: {
              amount: 0.3,
            },
          },
          "-=.3"
      );

      const card = gsap.timeline({
        paused: "true",
        reversed: "true",
      });
      card.fromTo(
          "#card-animation #card-plus",
          {
            display: "block",
          },
          {
            display: "none",
          }
      );
      card.fromTo(
          "#card-animation #card-minus",
          {
            display: "none",
          },
          {
            display: "block",
          }
      );
      card.fromTo(
          ".card-paragraph",
          {
            opacity: 0,
            y: 20,
          },
          {
            opacity: 1,
            y: 0,
            stagger: {
              amount: 0.2,
            },
          },
          "-=2"
      );

      this.cardClick = () => {
        card.reversed() ? card.play() : card.reverse();
      }
    },
  }
}
</script>

<style scoped>


</style>