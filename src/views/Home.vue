<template>
  <div class="dashboard-container">
    <SideBarMenu />
    <div class="content" :class="{ 'content-min' : getMinimize }">
      <div class="middle-content">
        <PedidosChart/>
        <UsuariosActivosChart />
        <RegistroUsuariosChart />
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
import SalesGeneral from '@/components/SalesGeneral.vue'
export default {
  name: 'Home',
  components: {
    SideBarMenu,
    PedidosChart,
    UsuariosActivosChart,
    RegistroUsuariosChart,
    SalesGeneral
  },
  computed: {
    getMinimize() {
      return this.$store.state.minimized;
    }
  }
}
</script>
