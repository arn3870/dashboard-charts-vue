<script>
import { ref, watchEffect, onBeforeUnmount } from "vue";
import ApexCharts from "apexcharts";

export default {
  props: {
    series: Array,
    options: Object,
  },
  setup(props) {
    const chartRef = ref(null);
    watchEffect(() => {
      const chartOptions = {
        ...props.options,
        series: props.series,
        chart: {
          ...(props.options && props.options.chart), // Copy chart-specific options
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
    <div ref="chartRef"></div>
  </div>
</template>