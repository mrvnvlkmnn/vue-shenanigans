<script>
import Card from './components/CardComponent.vue'
export default {
  components: {
    Card: Card
  },
  data() {
    return {
      currentCard: [],
      topValueCards: -50,
    }
  },
  methods: {
    handleMouseDown(e) {
      if (e.target.classList[0] === "card") {
        this.currentCard = e.target;
        window.addEventListener("pointermove", this.moveCard);
      }
    },
    handleMouseUp() {
      window.removeEventListener("pointermove", this.moveCard);
    },
    moveCard(event) {
      const { clientX, clientY } = event;

      this.currentCard.animate(
        {
          left: `${clientX}px`,
          top: `${clientY}px`,
        },
        { duration: 1500, fill: "forwards" }
      );
    },
    moveCards() {
      this.topValueCards = 50;
    }
  }
}
</script>

<template>
  <button @click="moveCards">Click me</button>
  <div class="card_container" @mousedown="handleMouseDown" @mouseup="handleMouseUp">
    <Card msg="Hello" left="35" :top="topValueCards"/>
    <Card msg="Test" left="45" :top="topValueCards"/>
    <Card msg="Moin" left="55" :top="topValueCards"/>
    <Card msg="Hilfe" left="65" :top="topValueCards"/>
  </div>
</template>

<style>
body {
  background-color: black;
}
.card_container {
  position: fixed;
  width: 100%;
  height: 100%;
}
</style>
