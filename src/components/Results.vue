<template>
  <!-- <p>Reaction Time: {{ scoreTime }} ms - {{ rankReactionTime }}</p>
  <p>Marksman: {{ scorePrecision }} points - {{ rankMarksman }}</p> -->
  <p class="score">Score: {{ finalResult }} points</p>
  <p class="rank">Rank: {{ rank }}</p>
</template>

<script>
export default {
    name: 'Results',
    props: ['scoreTime', 'scorePrecision', 'finalResult'],
    data() {
      return {
        rank: null,
        rankReactionTime: null,
        rankMarksman: null
      }
    },
    mounted() {

      if(this.finalResult < 7) {
        this.rank = "Dude, you are slow as hell!"
      }
      else if(this.finalResult < 10) {
        this.rank = "Fast as a snail!"
      }
      else if(this.finalResult < 14) {
        this.rank = "Quite average!"
      }
      else {
        this.rank = "Eagle eye!!!"
      }
    }
}
</script>

<style>
.rank {
  font-size: 30px;
  color: rgb(29, 59, 99);
  font-weight: 600;
}
.score {
  font-size: 20px;
  color: rgb(29, 59, 99);
  font-weight: 600;
}

</style>