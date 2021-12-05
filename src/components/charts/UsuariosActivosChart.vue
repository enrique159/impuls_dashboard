<template>
  <div class="container">
    <div class="header">
      <div class="title">
        <span>Usuarios Activos</span>
      </div>
      <DropdownButtonWhite />
    </div>
    <div class="usuarios-registros mt-3">
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
      type="bar"
      width="100%"
      :options="chartOptions"
      :series="series"
    ></apexchart>
  </div>
</template>

<script>
import DropdownButtonWhite from "@/components/DropdownButtonWhite.vue";
export default {
  name: "UsuariosActivosChart",
  components: {
    DropdownButtonWhite,
  },
  data() {
    return {
      catalogosVentas: [
        {
          id: 1,
          name: "Activos",
          color: "#60C788",
        },
        {
          id: 2,
          name: "Registros de pedidos",
          color: "#2475D3",
        },
      ],
      series: [
        {
          name: "Activos",
          data: [44, 55, 36, 41, 67, 22],
        },
        {
          name: "Registros de pedidos",
          data: [13, 23, 10, 20, 8, 13],
        },
      ],
      chartOptions: {
        chart: {
          type: "bar",
          height: 350,
          stacked: true,
          toolbar: {
            show: false,
          },
        },
        dataLabels: {
          enabled: false,
        },
        legend: {
          show: false,
        },
        plotOptions: {
          bar: {
            horizontal: false,
          },
        },
        colors: ["#60C788", "#2475D3"],
        xaxis: {
          type: "datetime",
          categories: [
            "01/01/2021 GMT",
            "01/05/2021 GMT",
            "01/10/2021 GMT",
            "01/15/2021 GMT",
            "01/20/2021 GMT",
            "01/25/2021 GMT",
          ],
        },
      },
    };
  },
};
</script>

<style lang="scss" scoped>
.container {
  width: 49%;
  margin-top: 48px;
  // HEADR //////////////////////
  .header {
    display: flex;
    justify-content: space-between;
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
  // USUARIOS REGISTROS //////////////////////
  .usuarios-registros {
    display: flex;
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
}
</style>