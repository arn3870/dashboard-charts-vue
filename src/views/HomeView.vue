<script>
import { ref, watchEffect, onBeforeUnmount } from "vue";
import ApexCharts from "apexcharts";
import StatusCards from "../components/StatusCards.vue";
import ReusbaleChart from "../components/reusbaleChart.vue";
import BarChart from "../components/BarChart.vue";
import PieChart from "../components/PieChart.vue";

export default {
  components: { StatusCards, ReusbaleChart, BarChart, PieChart },
  setup() {
    const series = [
      {
        name: "series1",
        data: [0, 2, 1.5, 3, 2, 3, 1, 2, 2.5, 2, 2.5, 3],
        color: "#22519F", // Set the color here
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
        { heading: "All tickets", statNumber: 752 },
        { heading: "Unassigned", statNumber: 68 },
        { heading: "Open", statNumber: 221 },
        { heading: "Solved", statNumber: 302 },
        { heading: "Critical", statNumber: 10 },
        { heading: "Orders", statNumber: 10 },
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
        <div
          class="mt-[10px] ml-[20px] mr-[20px] flex flex-row items-center justify-between"
        >
          <div class="chart-header-text">
            <p class="text-gray-400 text-sm">First response time</p>
            <h1 class="text-2xl font-bold">
              2 hours and 10 minutes
              <span class="text-red-400 text-xs">25%&#x2198;</span>
            </h1>
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
        <reusbale-chart :series="series" :options="options"></reusbale-chart>
      </div>
      <div class="bg-white min-h-[265px] min-w-[500px] rounded-[15px]">
        <div
          class="mt-[10px] ml-[20px] mr-[20px] flex flex-row items-center justify-between"
        >
          <div class="chart-header-text">
            <p class="text-gray-400 text-sm">Full resolution time</p>
            <h1 class="text-2xl font-bold">
              1 hours and 55 minutes
              <span class="text-red-400 text-xs">25%&#x2198;</span>
            </h1>
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
        <reusbale-chart :series="series" :options="options"></reusbale-chart>
      </div>
    </div>
    <div class="mt-[20px]">
      <bar-chart></bar-chart>
    </div>
    <div class="mt-[20px]">
      <pie-chart></pie-chart>
    </div>
  </div>
</template>
