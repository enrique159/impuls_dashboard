<template>
  <div class="content">
    <div class="header">
      <div class="title">
        <span>Ventas</span>
      </div>
      <DropdownButton />
    </div>
    <div class="circle-chart">
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
      <div class="chart">
        <div class="main-sales">
          <h4>{{ getMainSales }}%</h4>
          <span>{{ getMainSalesLabel }}</span>
        </div>
        <apexchart
          ref="realtimeChart"
          type="donut"
          :options="chartOptions"
          :series="series[0].data"
        ></apexchart>
      </div>
    </div>
    <div class="sales">
      <div class="total-sales">
        <div class="total-sales-title">
          <span>Total de ventas</span>
        </div>
        <div class="total-sales-value">
          <span>{{ getTotalSales }}</span>
        </div>
      </div>
      <div class="total-growth">
        <div class="total-growth-title">
          <span>% Crecimiento</span>
          <span class="total-growth-subtitle">Al mes anterior</span>
        </div>
        <div class="total-growth-value">
          <div class="arrow-up"></div>
          <span>9.4</span>
        </div>
      </div>
    </div>
    <div class="catalog">
      <table>
        <tr class="catalog-titles">
          <th>Catalogo</th>
          <th class="pedidos">Pedidos</th>
          <th class="total">Total</th>
        </tr>
        <tr v-for="item in catalogosVentas" :key="item.id">
          <td class="name">
            <div
              class="box-color"
              :style="'background-color:' + item.color + ';'"
            ></div>
            {{ item.name }}
          </td>
          <td class="pedidos">{{ item.pedidos }}</td>
          <td class="total">{{ formatMoney(item.salesAnual) }}</td>
        </tr>
      </table>
    </div>
    <button class="generate-report">
      <i class="ri-file-chart-fill pt-1"></i>
      Generar reporte
    </button>
  </div>
</template>

<script>
import DropdownButton from "@/components/DropdownButton.vue";
export default {
  name: "SalesGeneral",
  components: {
    DropdownButton,
  },
  data() {
    return {
      catalogosVentas: [
        {
          id: 1,
          name: "Otoño Invierno 2021",
          salesAnual: 110893.8,
          pedidos: 360,
          color: "#68757C",
        },
        {
          id: 2,
          name: "Promociones y descuentos",
          salesAnual: 23896.34,
          pedidos: 120,
          color: "#3A4253",
        },
      ],
      series: [
        {
          name: "value",
          data: [],
        },
      ],
      chartOptions: {
        labels: ["Otoño Invierno 2021", "Promociones y descuentos"],
        chart: {
          type: "donut",
        },
        dataLabels: {
          enabled: false,
        },
        colors: ["#68757C", "#3A4253"],
        legend: {
          show: false,
        },
      },
    };
  },
  created() {
    this.getPercentage();
  },
  methods: {
    formatMoney(total) {
      return new Intl.NumberFormat("es-MX", {
        style: "currency",
        currency: "MXN",
      }).format(total);
    },
    getPercentage() {
      //Get the percent of each sale from the total and push it into an array
      let total = 0;
      let newData = [];
      this.catalogosVentas.forEach((catalogo) => {
        total += catalogo.salesAnual;
      });
      this.catalogosVentas.forEach((catalogo) => {
        let percent = (catalogo.salesAnual * 100) / total;
        //give me only two decimals
        percent = percent.toFixed(2);
        percent = parseFloat(percent);
        newData.push(percent);
      });
      // const newData = this.series[0].data.map((e, index) => {
      //   // this.catalogosVentas.forEach((catalogo) => {
      //   //   let percent = (catalogo.salesAnual * 100) / total;
      //   //   //give me only two decimals
      //   //   percent = percent.toFixed(2);
      //   // });
      //   let percent = (this.catalogosVentas[index].salesAnual * 100) / total;
      //   percent = percent.toFixed(2);
      //   percent = parseFloat(percent);
      //   return percent
      // })
      console.log(newData);
      //this.series = [{ data: newData }];
      this.updateSeriesLine(newData);
    },
    updateSeriesLine(Data) {
      this.series = [{ data: Data }];
    },
  },
  computed: {
    getMainSales() {
      //Get the highest value from the array
      let max = Math.max(...this.series[0].data);
      return max;
    },
    getMainSalesLabel() {
      //Get the label of the highest value from the array
      let max = Math.max(...this.series[0].data);
      let index = this.series[0].data.indexOf(max);
      return this.chartOptions.labels[index];
    },
    getTotalSales() {
      let total = 0;
      this.catalogosVentas.forEach((catalogo) => {
        total += catalogo.salesAnual;
      });
      //convert a number in money format
      return this.formatMoney(total);
    },
  },
};
</script>

<style lang="scss" scoped>
.content {
  border-left: 1px solid #ccc;
  box-sizing: border-box;
  flex-direction: column;
  position: relative;
  display: flex;
  padding: 24px;
  padding-top: 48px;
  height: 100%;
  width: 30%;

  // HEADR //////////////////////
  .header {
    display: grid;
    grid-template-columns: 1fr auto;
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
  }

  // CHART //////////////////////
  .circle-chart {
    display: block;
    margin-top: 24px;
    .sales-options {
      display: flex;
      align-items: center;
      justify-content: flex-start;
      position: relative;
      padding: 2px 10%;
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
    .chart {
      position: relative;
      .main-sales {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        h4 {
          font-size: 1.5rem;
          font-weight: 900;
          margin: 0;
        }
        span {
          font-size: 0.7rem;
          font-weight: 600;
          margin: 0;
        }
      }
    }
  }

  // SALES //////////////////////
  .sales {
    margin-top: 24px;
    .total-sales {
      display: flex;
      justify-content: space-between;
      align-items: center;
      .total-sales-title {
        display: flex;
        align-items: center;
        justify-content: flex-start;
        span {
          font-size: 1rem;
          font-weight: 800;
        }
      }
      .total-sales-value {
        display: flex;
        align-items: center;
        justify-content: flex-start;
        span {
          font-size: 1.2rem;
          font-weight: 600;
        }
      }
    }
    .total-growth {
      margin-top: 6px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      .total-growth-title {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        justify-content: center;
        span {
          font-size: 1rem;
          font-weight: 800;
        }
        .total-growth-subtitle {
          font-size: 0.7rem;
          font-weight: 600;
          color: #68757c;
        }
      }
      .total-growth-value {
        display: flex;
        align-items: center;
        justify-content: flex-start;
        column-gap: 0.3rem;
        .arrow-up {
          width: 0;
          height: 0;
          border-left: 5px solid transparent;
          border-right: 5px solid transparent;
          border-bottom: 5px solid rgb(27, 226, 153);
        }
        span {
          font-size: 1rem;
          font-weight: 600;
        }
      }
    }
  }

  // CATALOG //////////////////////
  .catalog {
    margin-top: 24px;
    table {
      width: 100%;
      border-collapse: collapse;
      tr {
        th {
          height: 48px;
          text-align: left;
          font-size: 0.9rem;
          font-weight: 800;
          color: #9f9f9f;
        }
        td {
          height: 24px;
          text-align: left;
          font-size: 0.8rem;
          font-weight: 700;
        }
        .name {
          text-decoration: underline;
          position: relative;
          .box-color {
            position: absolute;
            left: -10px;
            top: 6px;
            width: 4px;
            height: 16px;
          }
        }
        .total,
        .pedidos {
          text-align: right;
        }
      }
    }
  }

  // BUTTON REPORT //////////////////
  .generate-report {
    position: absolute;
    width: 180px;
    bottom: 12px;
    left: calc(50% - 90px);
    background-color: black;
    border-radius: 12px;
    border: none;
    color: white;
    padding: 8px 16px 10px;
  }
}
</style>