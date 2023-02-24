<script>
export default {
  props: {
    msg: {
      type: String,
      required: true
    },
    left: {
      type: Number,
      required: true,
    },
    top: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      randomDegree: 0,
    }
  },
  beforeMount() {
    this.randomDegree = this.getRandomInt(-2, 7);
  },
  methods: {
    getRandomInt(min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min + 1) + min);
    }
  }
}
</script>


<template>
  <div class="card" :style="{ 'transform': 'rotate(' + randomDegree + 'deg)', 'left': left + '%', 'top': top + '%'}">{{ msg }}</div>
</template>

<style scoped lang="scss">
.card {
  background-color: white;
  font-size: 2rem;
  border-radius: 0.75rem;
  width: 288px;
  height: 384px;
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  user-select: none;
  translate: -50% -50%;
  transition: top 1.5s;
  
  filter: drop-shadow(0 0 0.75rem black);
}
</style>
