<template>
  <div class="dashboard-container">
    <SideBarMenu />
    <div class="content" :class="{ 'content-min' : getMinimize }">
      <div class="middle-content">
        <PedidosChart/>
      </div>
      <SalesGeneral />
    </div>
  </div>
</template>

<script>
import SideBarMenu from '@/components/SideBarMenu.vue'
import PedidosChart from '@/components/charts/PedidosChart.vue'
import SalesGeneral from '@/components/SalesGeneral.vue'
export default {
  name: 'Home',
  components: {
    SideBarMenu,
    PedidosChart,
    SalesGeneral
  },
  computed: {
    getMinimize() {
      return this.$store.state.minimized;
    }
  }
}
</script>
