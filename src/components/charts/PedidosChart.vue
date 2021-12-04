<template>
  <div>
    <apexchart
      width="500"
      type="area"
      :options="options"
      :series="series"
    ></apexchart>
  </div>
</template>

<script>
export default {
  name: "PedidosChart",
  data() {
    return {
      options: {
        chart: {
          id: "vuechart-example",
          zoom: {
            enabled: false
          },
        },
        dataLabels: {
          enabled: false
        },
        xaxis: {
          categories: ['1 Oct', '7 Oct', '15 Oct', '23 Oct', '30 Oct'],
        },
      },
      series: [
        {
          name: "series-1",
          data: [30, 40, 45, 50, 49],
        },
      ],
    };
  },
};
</script>

<style lang="scss" scoped>
</style>