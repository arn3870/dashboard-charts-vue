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
    const series = [44, 55, 13, 43, 22];
    const options = {
      chart: {
        width: 380,
        type: "pie",
      },
      labels: ["Team A", "Team B", "Team C", "Team D", "Team E"],
      responsive: [
        {
          breakpoint: 480,
          options: {
            chart: {
              width: 200,
            },
          },
        },
      ],
      legend: {
        show: false,
        position: "bottom",
      },
      stroke: {
        show: false,
      },
      colors: ["#1E529E", "#4594CD", "#52A5DB", "#62C1ED", "#98DDFA"],
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
  <div class="w-[100%] min-h-[400px] bg-white rounded-[15px] mb-20">
    <div
      class="mt-[10px] ml-[20px] pt-[20px] mr-[20px] flex flex-row items-center justify-between"
    >
      <div class="chart-header-text">
        <h1 class="text-2xl font-bold">Ticket activity</h1>
      </div>
      <div>
        <select
          class="border-none text-sm text-gray-700 py-1 pl-3 pr-1 rounded focus:outline-none focus:ring"
        >
          <option>This Year</option>
          <option>This Month</option>
          <option>This Week</option>
        </select>
      </div>
    </div>
    <div class="w-4/5 mx-auto h-[1px] bg-gray-300 mt-10 mb-5"></div>
    <div class="items-center" ref="chartRef"></div>
  </div>
</template>
