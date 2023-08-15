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
        color: "#2E6BAE",
      },
      {
        name: "Revenue",
        data: [76, 85, 101, 98, 87, 105, 91, 114, 94],
        color: "#BBDD52",
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
          borderRadius: 5,
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
      yaxis: {},
      legend: {
        show: false,
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
  <div class="bg-white w-[100%] min-h-[400px] pt-[10px]">
    <div class="ml-[30px] mr-[30px] flex flex-row justify-between">
      <div>
        <h1 class="text-2xl font-bold">Tickets solved and created</h1>
        <div class="flex flex-row">
          <div class="flex flex-col mr-[20px]">
            <p class="text-gray-400">Created</p>
            <div class="flex flex-row items-center">
              <div class="w-1.5 h-1.5 rounded-full bg-[#2E6BAE] mr-[5px]"></div>
              <div class="font-bold">
                986 <span class="text-green-500 text-[12px]">25%&#8599;</span>
              </div>
            </div>
          </div>
          <div class="flex flex-col">
            <p class="text-gray-400">Solved</p>
            <div class="flex flex-row items-center">
              <div class="w-1.5 h-1.5 rounded-full bg-[#BBDD52] mr-[5px]"></div>
              <div class="font-bold">
                1132 <span class="text-green-500 text-[12px]">25%&#8599;</span>
              </div>
            </div>
          </div>
        </div>
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
    <div ref="chartRef"></div>
  </div>
</template>
