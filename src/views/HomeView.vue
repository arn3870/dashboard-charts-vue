<script>
import { ref, watchEffect, onBeforeUnmount } from 'vue';
import ApexCharts from 'apexcharts';
import StatusCards from '../components/StatusCards.vue';

export default {
  components: { StatusCards },
  // props: {
  //   series: Array,
  //   options: Object,
  // },
  setup(props) {
    const chartRef = ref(null);
    const series = [
    {
      name: 'series1',
      data: [45, 52, 38, 24, 33, 46, 54],
      color: '#50C878', // Set the color here
    },
  ];

  const options = {
    chart: {
      type: 'area',
      height: 350,
      width: 716,
      toolbar: {
        show: false, // Hide chart toolbar
      },
    },
    dataLabels: {
      enabled: false, // Disable data labels
    },
    stroke: {
      curve: 'smooth',
    },
    xaxis: {
      axisBorder: {
        show: true,
        color: '#F2F5FE', // Set x-axis border color
      },
      categories: ['jan', 'feb', 'mar', 'apr', 'may', 'jun', 'jul', 'aug'],
    },
    yaxis: {
      axisBorder: {
        show: true,
        color: '#F2F5FE', // Set y-axis border color
      },
    },
    grid: {
      show: false, // Hide grid lines
    },
  };

    watchEffect(() => {
      const chartOptions = {
        ...options,
        series: series,
        chart: {
          ...(options && options.chart), // Copy chart-specific options
          id: 'gross-revenue-chart',
        },
      };

      const chart = new ApexCharts(chartRef.value, chartOptions);
      chart.render();

      onBeforeUnmount(() => {
        chart.destroy();
      });
    });

    return {
      chartRef,
    };
  },
};
</script>

<template>
  <div class="wrapper">
    <status-cards></status-cards>
    <div ref="chartRef"></div>
  </div>
</template>

<style scoped>
.weapper{
  display: flex;
  flex-direction: column;
}
</style>