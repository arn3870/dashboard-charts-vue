<script>
import { ref, watchEffect, onBeforeUnmount } from "vue";
import ApexCharts from "apexcharts";

export default {
  setup() {
    const chartRef = ref(null);
    const series = [
      {
        name: "Net Profit",
        data: [44, 55, 57, 56, 61, 58, 63, 60, 66],
        color: "#224c98"
      },
      {
        name: "Revenue",
        data: [76, 85, 101, 98, 87, 105, 91, 114, 94],
        color: "#A2FF84"
      },
    ];

    const options = {
      chart: {
        type: "bar",
        height: 350,
        width: 1000,
        toolbar: {
          show: false, // Hide chart toolbar
        },
      },
      plotOptions: {
        bar: {
          horizontal: false,
          columnWidth: "25%",
          borderRadius: 5
        },
      },
      dataLabels: {
        enabled: false,
      },
      stroke: {
        show: true,
        width: 2,
        colors: ["transparent"],
      },
      xaxis: {
        categories: [
          "Feb",
          "Mar",
          "Apr",
          "May",
          "Jun",
          "Jul",
          "Aug",
          "Sep",
          "Oct",
        ],
      },
      yaxis: {
      },
      fill: {
        opacity: 1,
      },
      tooltip: {
        y: {
          formatter: function (val) {
            return "$ " + val + " thousands";
          },
        },
      },
    };
    watchEffect(() => {
      const chartOptions = {
        ...options,
        series: series,
        chart: {
          ...(options && options.chart), // Copy chart-specific options
          id: "gross-revenue-chart",
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

<style scoped>
.wrapper {
  background: white;
  height: 400px;
  width: 100%;
  border-radius: 15px;
}
</style>
