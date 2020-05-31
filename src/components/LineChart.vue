<script>
import { Line } from 'vue-chartjs';

const setDegreeCelsius = (value, index, values) => {
  console.log(value, index, values)
  return `${value}℃`
}

export default {
  extends: Line,
  name: 'LineChart',
  data:() => ({
    chartdata: {
      labels: ["12:00", "15:00", "18:00", "21:00", "0:00", "3:00", "6:00", "9:00"],
      datasets: [
        {
          label: 'temperature',
          data: [23, 25, 22, 20, 19, 19, 19, 20, 23],
          borderColor: 'rgba(255, 146, 51, 1)',
          backgroundColor: 'rgba(255, 146, 51, 0.2)',
        }
      ]
    },
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
  mounted () {
    this.renderChart(this.chartdata, this.options);
  }
}
</script>
