<template>
  <div class="home">
    <LineChart/>
  </div>
</template>

<script>
// @ is an alias to /src
import LineChart from "@/components/LineChart.vue";

export default {
  name: 'Home',
  components: {
    LineChart
  },
  mounted() {
    console.log('mounted')
  }
}
</script>
