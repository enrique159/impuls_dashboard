<template>
  <div style="width: 100%;">
    <div class="header">
      <div class="title">
        <span>Pedidos</span>
      </div>
      <div class="generals">
        <span class="daily-avg"
          >%Dia: <b>{{ getDailyAverage }}</b></span
        >
        <span class="total">Total: <b>{{ getTotal }}</b></span>
      </div>
      <DropdownButtonWhite />
    </div>
    <div class="catalogo-pedidos mt-3">
      <div
        v-for="catalogo in catalogosVentas"
        :key="catalogo.id"
        class="sales-options"
      >
        <div
          class="circle-option"
          :style="'background-color:' + catalogo.color + ';'"
        ></div>
        <span>{{ catalogo.name }}</span>
      </div>
    </div>
    <apexchart
      width="100%"
      height="200"
      type="area"
      :options="options"
      :series="series"
    ></apexchart>
  </div>
</template>

<script>
import DropdownButtonWhite from "@/components/DropdownButtonWhite.vue";
export default {
  name: "PedidosChart",
  components: {
    DropdownButtonWhite,
  },
  data() {
    return {
      catalogosVentas: [
        {
          id: 1,
          name: "Otoño Invierno 2021",
          salesAnual: 110893.8,
          pedidos: 360,
          color: "#6AD9D9",
        },
      ],
      options: {
        chart: {
          id: "vuechart-example",
          zoom: {
            enabled: false,
          },
        },
        colors: ["#6AD9D9"],
        fill: {
          type: "solid",
        },
        dataLabels: {
          enabled: false,
        },
        xaxis: {
          type: "datetime",
          categories: [
            "01/01/2011 GMT",
            "01/05/2011 GMT",
            "01/10/2011 GMT",
            "01/15/2011 GMT",
            "01/20/2011 GMT",
            "01/25/2011 GMT",
            "01/30/2011 GMT",
          ],
        },
      },
      series: [
        {
          name: "series-1",
          data: [44, 55, 41, 67, 22, 43, 60],
        },
      ],
    };
  },
  computed: {
    getDailyAverage() {
      // get the average of the data series
      let average =
        this.series[0].data.reduce((acc, curr) => acc + curr, 0) /
        this.series[0].data.length;
      average = average.toFixed(2);
      return average;
    },
    getTotal() {
      // get the total of the data series
      let total = this.series[0].data.reduce((acc, curr) => acc + curr, 0);
      return total;
    },
  },
};
</script>

<style lang="scss" scoped>
// HEADR //////////////////////
.header {
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
.catalogo-pedidos {
  .sales-options {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    position: relative;
    padding: 2px 12px;
    .circle-option {
      width: 14px;
      height: 14px;
      border-radius: 50%;
      background-color: #68757c;
    }
    span {
      font-size: 0.8rem;
      font-weight: 600;
      margin-left: 10px;
    }
  }
}
</style>