<template>
  <div class="w-100">
    <div class="header">
      <div class="title">
        <span>Ventas</span>
      </div>
      <div class="generals">
        <span class="daily-avg"
          >%Dia: <b>{{ getDailyAverage }}</b></span
        >
        <span class="total">Total: <b>{{ getTotal }}</b></span>
      </div>
      <DropdownButtonWhite />
    </div>
    <apexchart
      type="area"
      height="200"
      :options="chartOptions"
      :series="series"
    ></apexchart>
  </div>
</template>

<script>
import DropdownButtonWhite from "@/components/DropdownButtonWhite.vue";
export default {
  name: "VentasChart",
  components: {
    DropdownButtonWhite
  },
  data() {
    return {
      series: [
        {
          name: "Sales",
          data: [
            8548, 12467.1, 6652, 5021, 6240, 12485, 11620.04, 13856, 11658, 18156,
            11496, 7896, 8695,
          ],
        },
      ],
      chartOptions: {
        chart: {
          type: "area",
          zoom: {
            enabled: false,
          },
        },
        colors: ["#5900ff"],
        dataLabels: {
          enabled: false,
        },
        stroke: {
          curve: "straight",
        },
        xaxis: {
          type: "datetime",
          categories: [
            "01/01/2021 GMT",
            "01/03/2021 GMT",
            "01/05/2021 GMT",
            "01/07/2021 GMT",
            "01/10/2021 GMT",
            "01/13/2021 GMT",
            "01/15/2021 GMT",
            "01/17/2021 GMT",
            "01/20/2021 GMT",
            "01/23/2021 GMT",
            "01/25/2021 GMT",
            "01/27/2021 GMT",
            "01/30/2021 GMT",
          ],
        },
        legend: {
          horizontalAlign: "left",
        },
      },
    };
  },
  methods: {
    formatMoney(total) {
      return new Intl.NumberFormat("es-MX", {
        style: "currency",
        currency: "MXN",
      }).format(total);
    },
  },
  computed: {
    getDailyAverage() {
      // get the average of the data series
      let average =
        this.series[0].data.reduce((acc, curr) => acc + curr, 0) /
        this.series[0].data.length;
      average = average.toFixed(2);
      average = parseInt(average);
      average = this.formatMoney(average);
      return average;
    },
    getTotal() {
      // get the total of the data series
      let total = this.series[0].data.reduce((acc, curr) => acc + curr, 0);
      return this.formatMoney(total);
    },
  }
};
</script>

<style lang="scss" scoped>
// HEADR //////////////////////
.header {
  margin-top: 48px;
  display: grid;
  grid-template-columns: 1fr 1fr auto;
  align-items: center;

  .title {
    height: 20px;
    padding-left: 24px;
    position: relative;
    span {
      font-size: 1.1rem;
      font-weight: 700;
    }
    &::before {
      content: "";
      position: absolute;
      left: 0;
      top: 0;
      width: 4px;
      height: 100%;
      background-color: #000000;
    }
  }
  .generals {
    display: flex;
    align-items: center;
    justify-content: space-around;
  }
}
</style>
