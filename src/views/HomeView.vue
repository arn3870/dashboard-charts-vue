<script>
import { ref, watchEffect, onBeforeUnmount } from "vue";
import ApexCharts from "apexcharts";
import StatusCards from "../components/StatusCards.vue";
import ReusbaleChart from "../components/reusbaleChart.vue";

export default {
  components: { StatusCards, ReusbaleChart },
  // props: {
  //   series: Array,
  //   options: Object,
  // },
  setup(props) {
    const series = [
      {
        name: "series1",
        data: [0, 1, 2, 3],
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
        categories: ["jan", "feb", "mar", "apr", "may", "jun", "jul", "aug", 'sep', 'oct', 'nov', 'dec'],
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
    <div class="status-card">
      <status-cards
        v-for="(card, index) in statusData"
        :key="index"
        :heading="card.heading"
        :statNumber="card.statNumber"
      ></status-cards>
    </div>
    <div class="stat-charts">
      <reusbale-chart :series="series" :options="options"></reusbale-chart>
      <reusbale-chart :series="series" :options="options"></reusbale-chart>
    </div>
  </div>
</template>

<style scoped>
.weapper {
  display: flex;
  flex-direction: column;
}
.status-card {
  display: flex;
  flex-direction: row;
}
.stat-charts{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
</style>
