<template>
  <div class="home">
    <LineChartContainer/>
  </div>
</template>

<script>
// @ is an alias to /src
import LineChartContainer from "@/components/LineChartContainer.vue";

export default {
  name: 'Home',
  components: {
    LineChartContainer
  },
}
</script>
