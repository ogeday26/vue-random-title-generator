<template>
  <div class="container">
    <span class="title">{{ title }}</span>
    <button class="btn" @click="this.title = this.getRandom()">New Title</button>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';

export default {
  data() {
    return {
      title: 'Generated Title',
    };
  },
  computed: {
    ...mapGetters([
      'getLevels',
      'getFields',
      'getSubfields',
      'getSpecialties',
      'getDayJobs',
      'getSuffixes',
    ]),
  },
  mounted() {
    this.title = this.getRandom();
  },
  methods: {
    coinToss() {
      return Math.floor(Math.random() * 2) === 0;
    },
    choice(fromArray) {
      return fromArray[Math.floor(Math.random() * fromArray.length)];
    },
    getRandom() {
      const titleComponents = [];
      if (this.coinToss()) {
        titleComponents.push(this.choice(this.getLevels));
      }
      if (this.coinToss()) {
        titleComponents.push(this.choice(this.getFields));
      }
      if (this.coinToss()) {
        titleComponents.push(this.choice(this.getSubfields));
      }
      if (this.coinToss() || this.coinToss()) {
        titleComponents.push(this.choice(this.getSpecialties));
      }
      titleComponents.push(this.choice(this.getDayJobs));
      if (this.coinToss() && this.coinToss()) {
        titleComponents.push(this.choice(this.getSuffixes));
      }
      return titleComponents.join(' ');
    },
  },
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Nunito:wght@600&display=swap');

body {
  background-color: rgba(192, 196, 231, 0.76);
}
.container {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  height: 100vh;
  flex-direction: column;
}
.title {
  font-family: 'Nunito', sans-serif;
  font-size: 4rem;
}
.btn {
  background-color:#44c767;
  border-radius:40px;
  border:1px solid #18ab29;
  display:inline-block;
  cursor:pointer;
  color:#ffffff;
  font-family:Arial;
  font-size:40px;
  padding:10px 70px;
  text-decoration:none;
  text-shadow:0px 0px 0px #2f6627;
}
.btn:hover {
  background-color:#5cbf2a;
}
.btn:active {
  position:relative;
  top:1px;
}
</style>
