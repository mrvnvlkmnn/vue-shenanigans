<script>
import Card from './components/CardComponent.vue'
export default {
    components: {
        Card: Card
    },
    data() {
        return {
            currentCard: [],
            topValueCards: 150,
            containerOpacity: 1
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
                { duration: 1000, fill: "forwards" }
            );


        },
        showCards() {
            this.containerOpacity = 1;
            this.topValueCards = 50;
        },
        hideCards() {
            this.containerOpacity = 0;
            const cards = document.getElementsByClassName('card');
            setTimeout(() => {
                for (let card of cards) {
                    if (card.getAnimations().length != 0) {
                        card.getAnimations()[0].cancel();
                    }
                }
                this.topValueCards = 150;
            }, 1500);
        }
    }
}
</script>

<template>
    <button @click="showCards">Click me</button>
    <button @click="hideCards">Click me</button>
    <div class="card_container" :style="{ opacity: containerOpacity, }" @mousedown="handleMouseDown"
        @mouseup="handleMouseUp">
        <Card msg="Hello" :left="35" :top="topValueCards" :transitionDelay="0" />
        <Card msg="Test" :left="45" :top="topValueCards" :transitionDelay="0.2" />
        <Card msg="Moin" :left="55" :top="topValueCards" :transitionDelay="0.4" />
        <Card msg="Hilfe" :left="65" :top="topValueCards" :transitionDelay="0.6" />
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
    opacity: 1;
    transition: opacity 1s;

}
</style>
