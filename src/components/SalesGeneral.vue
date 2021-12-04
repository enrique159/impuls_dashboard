<template>
  <div class="content">
    <div class="header">
      <div class="title">
        <span>Ventas</span>
      </div>
      <button class="choose-button">{{ btnSelected[1] }}</button>
    </div>
    <div class="circle-chart">
      <apexchart type="donut" :options="chartOptions" :series="series"></apexchart>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'SalesGeneral',
    data() {
      return {
        btnSelected: [
          'Anual',
          'Mensual',
          'Semanal',
          'Diario'
        ],
        series: [80, 20],
        chartOptions: {
          labels: ['Apple', 'Mango'],
          chart: {
            type: 'donut',
          },
          dataLabels: {
            enabled: false,
          },
          colors: ['#68757C', '#3A4253'],
          legend: {
            show: false,
          },
        },
      }
    },
    methods: {

    },
  }
</script>

<style lang="scss" scoped>
.content {
  border-left: 1px solid #ccc;
  box-sizing: border-box;
  flex-direction: column;
  display: flex;
  padding: 24px;
  height: 100%;
  width: 30%;

  .header {
    display: grid;
    grid-template-columns: 1fr auto;
    align-items: center;
    
    .title{
      height: 20px;
      padding-left: 24px;
      position: relative;
      span {
        font-size: 1.1rem;
        font-weight: 700;
      }
      &::before {
        content: '';
        position: absolute;
        left: 0;
        top: 0;
        width: 4px;
        height: 100%;
        background-color: #000000;
      }
    }

    .choose-button {
      background-color: rgb(0, 0, 0);
      border: none;
      border-radius: 4px;
      color: rgb(255, 255, 255);
      font-size: 0.8rem;
      font-weight: 700;
      height: 24px;
      padding: 0 8px;
      cursor: pointer;
    }
  }
}
</style>