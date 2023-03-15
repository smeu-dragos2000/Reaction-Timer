<template>
  <div class="target" @click="precisionDetector"></div>
</template>

<script>
export default {
    data() {
      return {
        precisionCircle: null
      }
    },
    name: 'TargetCircle',
    props: {precision: Number},
    
    methods: {
      precisionDetector() {
        this.precisionCircle = this.precision
        this.$emit('created', this.precisionCircle)
      },
    }
}

</script>

<style scoped>

.target {
        position: absolute;
        border-radius: 50%;
    }

</style>