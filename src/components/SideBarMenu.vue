<template>
  <div class="container" :class="{ 'container-minimized' : min }">
    <div class="head">
      <img src="@/assets/img/logo_white.png" alt="" class="logo" />
      <button class="minimize-bar d-flex j-center a-center" @click="min = !min">
        <img src="@/assets/icons/arrow-left.svg" alt="" />
      </button>
    </div>
    <div class="options">
      <div class="option" :class="{ 'option-active' : options.dashboard }" @click="changeOption('dashboard')">
        <img src="@/assets/icons/sidebar/dashboard.svg" alt="" class="icon">
        <span>Dashboard</span>
      </div>

      <div class="option" :class="{ 'option-active' : options.pedidos }" @click="changeOption('pedidos')">
        <img src="@/assets/icons/sidebar/pedidos.svg" alt="" class="icon">
        <span>Pedidos</span>
      </div>

      <div class="option" :class="{ 'option-active' : options.usuarios }" @click="changeOption('usuarios')">
        <img src="@/assets/icons/sidebar/user.svg" alt="" class="icon">
        <span>Usuarios</span>
      </div>

      <div class="option" :class="{ 'option-active' : options.catalogos }" @click="changeOption('catalogos')">
        <img src="@/assets/icons/sidebar/catalogo.svg" alt="" class="icon">
        <span>Catálogos</span>
      </div>

      <div class="option" :class="{ 'option-active' : options.reportes }" @click="changeOption('reportes'), despliega = !despliega">
        <img src="@/assets/icons/sidebar/reportes.svg" alt="" class="icon">
        <span>Reportes</span>
        <img src="@/assets/icons/arrow-down.svg" alt="" class="despliega" :class="{ 'rotated' : despliega }">
      </div>

      <div class="suboptions" :class="{ 'suboptions-active' : despliega}">
        <div class="suboption">
          <span>General</span>
        </div>
        <div class="suboption">
          <span>Pedidos</span>
        </div>
        <div class="suboption">
          <span>Usuarios</span>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: "SideBarMenu",
  data() {
    return {
      options: {
        dashboard: true,
        pedidos: false,
        usuarios: false,
        catalogos: false,
        reportes: false
      },
      despliega: false,
      min: false,
    }
  },
  methods: {
    changeOption(option) {
      this.options.dashboard = false;
      this.options.pedidos = false;
      this.options.usuarios = false;
      this.options.catalogos = false;
      this.options.reportes = false;
      this.options[option] = true;
    }
  },
};
</script>

<style lang="scss" scoped>
.container {
  background-color: black;
  transition: 0.3s ease-out;
  box-sizing: border-box;
  width: 240px;
  height: 100%;
  color: white;
  .head {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 24px;
    .logo {
      width: 98px;
    }
    .minimize-bar {
      background-color: rgba($color: #fff, $alpha: 0.1);
      transition: 0.2s ease-in-out;
      border-radius: 12px;
      cursor: pointer;
      padding: 0;
      width: 32px;
      height: 32px;
      border: none;
      img {
        width: 8px;
      }
      &:hover {
        background-color: rgba($color: #fff, $alpha: 0.2);
      }
    }
  }

  .options {
    display: flex;
    flex-direction: column;
    .option {
      display: flex;
      position: relative;
      align-items: center;
      border-radius: 12px;
      margin: 0 12px;
      padding: 12px;
      cursor: pointer;
      .icon {
        width: 16px;
        margin-right: 18px;
        transition: 0.2s ease-in-out;
        filter: opacity(0.6);
      }
      .despliega {
        position: absolute;
        transition: 0.3s ease-in-out;
        top: 18px;
        right: 16px;
        width: 12px;
      }
      .rotated {
        transform: rotate(180deg);
      }
      span {
        font-size: 1.1rem;
        font-weight: 800;
      }
      &:hover {
        .icon {
          margin-right: 24px;
        }
      }
    }
    .option-active {
      .icon {
        filter: opacity(1);
      }
    }
    .option-active::before {
      content: "";
      position: absolute;
      top: 10px;
      left: -8px;
      width: 4px;
      height: 24px;
      background-color: rgba($color: #fff, $alpha: 1.0);
    }
    .suboptions {
      transition: 0.2s ease-in-out;
      overflow: hidden;
      height: 0px;
      opacity: 0.5;
      .suboption {
        margin: 0 12px;
        padding: 8px;
        padding-left: 58px;
        cursor: pointer;
        filter: opacity(0.6);
        &:hover {
          filter: opacity(1);
        }
        span {
          font-size: 1.1rem;
          font-weight: 600;
        }
      }
    }
    .suboptions-active {
      opacity: 1;
      height: 200px;
    }
  }
}
.container-minimized{
  width: 60px;
  .head {
    padding: 24px 0;
    justify-content: center;
    .logo {
      display: none;
    }
    .minimize-bar {
      img {
        transform: rotate(180deg);
      }
    }
  }
  .options {
    .option {
      span, .despliega {
        opacity: 0;
      }
    }
  }
}
</style>