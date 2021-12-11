<template>
  <div class="dashboard-container">
    <SideBarMenu />
    <div class="content" :class="{ 'content-min' : getMinimize }">
      <div class="middle-content">
        <PedidosChart/>
        <UsuariosActivosChart />
        <RegistroUsuariosChart />
        <VentasChart />
      </div>
      <SalesGeneral />
    </div>
  </div>
</template>

<script>
import SideBarMenu from '@/components/SideBarMenu.vue'
import PedidosChart from '@/components/charts/PedidosChart.vue'
import UsuariosActivosChart from '@/components/charts/UsuariosActivosChart.vue'
import RegistroUsuariosChart from '@/components/charts/RegistroUsuariosChart.vue'
import VentasChart from '@/components/charts/VentasChart.vue'
import SalesGeneral from '@/components/SalesGeneral.vue'
export default {
  name: 'Home',
  components: {
    SideBarMenu,
    PedidosChart,
    UsuariosActivosChart,
    RegistroUsuariosChart,
    VentasChart,
    SalesGeneral
  },
  computed: {
    getMinimize() {
      return this.$store.state.minimized;
    }
  }
}
</script>
