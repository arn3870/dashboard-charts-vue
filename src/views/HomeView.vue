<script>
import { ref, watchEffect, onBeforeUnmount } from "vue";
import ApexCharts from "apexcharts";
import StatusCards from "../components/StatusCards.vue";
import ReusbaleChart from "../components/reusbaleChart.vue";
import BarChart from "../components/BarChart.vue";

export default {
  components: { StatusCards, ReusbaleChart, BarChart },
  // props: {
  //   series: Array,
  //   options: Object,
  // },
  setup(props) {
    const series = [
      {
        name: "series1",
        data: [0, 2, 1.5, 3, 2, 3, 1, 2, 2.5, 2, 2.5, 3],
        color: "#224c98", // Set the color here
      },
    ];

    const options = {
      chart: {
        type: "area",
        height: 250,
        width: 450,
        toolbar: {
          show: false, // Hide chart toolbar
        },
      },
      dataLabels: {
        enabled: false, // Disable data labels
      },
      stroke: {
        curve: "smooth",
      },
      xaxis: {
        axisBorder: {
          show: true,
          color: "#F2F5FE", // Set x-axis border color
        },
        categories: [
          "Jan",
          "Feb",
          "Mar",
          "Apr",
          "May",
          "Jun",
          "Jul",
          "Aug",
          "Sep",
          "Oct",
          "Nov",
          "Dec",
        ],
      },
      yaxis: {
        axisBorder: {
          show: true,
          color: "#F2F5FE", // Set y-axis border color
        },
      },
    };
    return {
      series,
      options,
      statusData: [
        { heading: "Total Users", statNumber: 1500 },
        { heading: "Total Users", statNumber: 1500 },
        { heading: "Revenue", statNumber: 50000 },
        { heading: "Revenue", statNumber: 50000 },
        { heading: "Orders", statNumber: 300 },
        { heading: "Orders", statNumber: 300 },
      ],
    };
  },
};
</script>

<template>
  <div class="wrapper">
    <div class="flex flex-row">
      <status-cards
        v-for="(card, index) in statusData"
        :key="index"
        :heading="card.heading"
        :statNumber="card.statNumber"
      ></status-cards>
    </div>
    <div class="flex flex-row justify-between">
      <div class="bg-white min-h-[265px] min-w-[500px] rounded-[15px]">
        <div class="mt-[10px] ml-[30px]">
          <div class="chart-header-text">
            <p class="text-gray-400 text-sm">First response time</p>
            <h1 class="text-2xl font-bold">
              2 hours and 10 minutes
              <span class="text-red-400 text-xs">25%&#x2198;</span>
            </h1>
          </div>
          <div></div>
        </div>
        <reusbale-chart :series="series" :options="options"></reusbale-chart>
      </div>
      <div class="bg-white min-h-[265px] min-w-[500px] rounded-[15px]">
        <div class="mt-[10px] ml-[30px]">
          <div class="chart-header-text">
            <p class="text-gray-400 text-sm">Full resolution time</p>
            <h1 class="text-2xl font-bold">
              1 hours and 55 minutes
              <span class="text-red-400 text-xs">25%&#x2198;</span>
            </h1>
          </div>
        </div>
        <reusbale-chart :series="series" :options="options"></reusbale-chart>
      </div>
    </div>
    <div class="mt-[20px]">
      <bar-chart></bar-chart>
    </div>
  </div>
</template>
