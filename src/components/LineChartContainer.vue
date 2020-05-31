<template>
  <div class="container">
    <LineChart
      v-if="loaded"
      :chartdata="chartdata"
      :options="options"/>
    <VueLoading v-else type="bars" color="rgb(255, 146, 51)" :size="{ width: '50px', height: '50px' }"/>
  </div>
</template>

<script>
import LineChart from '@/components/LineChart.vue';
import { VueLoading } from 'vue-loading-template'

const setDegreeCelsius = (value, index, values) => {
  return `${value}℃`
}

export default {
  name: 'LineChartContainer',
  components: {
    LineChart,
    VueLoading
  },
  data: () => ({
    loaded: false,
    chartdata: {},
    options: {
      scales: {
          yAxes: [{
              ticks: {
                  beginAtZero: true,
                  callback: function(value, index, values) {
                      return setDegreeCelsius(value, index, values);
                  }
              }
          }]
      },
      responsive: true,
      maintainAspectRatio: false
    }
  }),
  async mounted () {
    const url = 'http://localhost:3000/chartData';
    this.loaded = false

      try {
        const response = await fetch(url);
        const chartData = await response.json();

        const chartdata = this.createChartdata(chartData.temperature, chartData.labels);
        this.chartdata = chartdata;

        this.loaded = true
      } catch (e) {
        console.error('error', e)
      }
  },
  methods: {
    createChartdata(data, labels) {
      const chartdata = {
        labels: labels,
        datasets: [
          {
            label: 'temperature',
            data: data,
            borderColor: 'rgba(255, 146, 51, 1)',
            backgroundColor: 'rgba(255, 146, 51, 0.2)',
          }
        ]
      }
      return chartdata;
    }
  }
}
</script>
