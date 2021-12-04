<template>
  <div class="container" :class="{ 'container-minimized': min }">
    <div class="head">
      <img src="@/assets/img/logo_white.png" alt="" class="logo" />
      <button class="minimize-bar d-flex j-center a-center" @click="minimize()">
        <img src="@/assets/icons/arrow-left.svg" alt="" />
      </button>
    </div>
    <div class="options">
      <div
        class="option"
        :class="{ 'option-active': options.dashboard }"
        @click="changeOption('dashboard')"
      >
        <img src="@/assets/icons/sidebar/dashboard.svg" alt="" class="icon" />
        <span>Dashboard</span>
      </div>

      <div
        class="option"
        :class="{ 'option-active': options.pedidos }"
        @click="changeOption('pedidos')"
      >
        <img src="@/assets/icons/sidebar/pedidos.svg" alt="" class="icon" />
        <span>Pedidos</span>
      </div>

      <div
        class="option"
        :class="{ 'option-active': options.usuarios }"
        @click="changeOption('usuarios')"
      >
        <img src="@/assets/icons/sidebar/user.svg" alt="" class="icon" />
        <span>Usuarios</span>
      </div>

      <div
        class="option"
        :class="{ 'option-active': options.catalogos }"
        @click="changeOption('catalogos')"
      >
        <img src="@/assets/icons/sidebar/catalogo.svg" alt="" class="icon" />
        <span>Catálogos</span>
      </div>

      <div
        class="option"
        :class="{ 'option-active': options.reportes }"
        @click="changeOption('reportes'), (despliega = !despliega)"
      >
        <img src="@/assets/icons/sidebar/reportes.svg" alt="" class="icon" />
        <span>Reportes</span>
        <img
          src="@/assets/icons/arrow-down.svg"
          alt=""
          class="despliega"
          :class="{ rotated: despliega }"
        />
      </div>

      <div class="suboptions" :class="{ 'suboptions-active': despliega }">
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

    <div class="foot">
      <div class="config mb-3">
        <a href="#" class="mb-2">
          <i class="ri-settings-3-fill icono"></i>
          <span>Configuracion</span>
        </a>
        <a href="#">
          <i class="ri-question-line icono"></i>
          <span>Ayuda y soporte</span>
        </a>
      </div>
      <div class="profile">
        <div class="picture">
          <img src="@/assets/emojis/dog-eji.png" alt="" />
        </div>
        <div class="user-profile">
          <span class="name">Enrique Marin</span>
          <span class="username">enriquemarin</span>
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
        reportes: false,
      },
      despliega: false,
      min: false,
    };
  },
  methods: {
    changeOption(option) {
      this.options.dashboard = false;
      this.options.pedidos = false;
      this.options.usuarios = false;
      this.options.catalogos = false;
      this.options.reportes = false;
      this.options[option] = true;
    },
    minimize() {
      this.min = !this.min;
      this.$store.state.minimized = this.min;
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  background-color: black;
  transition: 0.3s ease-out;
  box-sizing: border-box;
  position: relative;
  width: 240px;
  height: 100%;
  color: white;
  overflow-x: hidden;
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
      background-color: rgba($color: #fff, $alpha: 1);
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
  .foot {
    width: 240px;
    box-sizing: border-box;
    position: absolute;
    bottom: 0;
    left: 0;
    .config {
      display: flex;
      flex-direction: column;
      padding: 12px 24px;
      a {
        color: #aaaaaa;
        text-transform: none;
        text-decoration: none;
        display: inline-block;
        font-weight: 600;
        height: 16px;
        &:hover {
          color: #fff;
        }
        span {
          opacity: 1;;
        }
        .icono {
          display: none;
        }
      }
    }
    .profile {
      width: 100%;
      display: flex;
      justify-content: flex-start;
      align-items: center;
      cursor: pointer;
      padding: 12px 16px;
      .picture {
        background-color: rgba($color: rgb(42, 182, 251), $alpha: 1);
        display: flex;
        justify-content: center;
        align-items: center;
        border-radius: 50%;
        margin-right: 12px;
        height: 36px;
        width: 36px;
        img {
          width: 24px;
        }
      }
      .user-profile {
        display: flex;
        flex-direction: column;
        .name {
          font-size: 1rem;
          font-weight: 900;
        }
        .username {
          font-size: 0.8rem;
          font-weight: 600;
          letter-spacing: 0.5px;
        }
      }
      &:hover{
        background-color: rgba($color: #fff, $alpha: 0.1);
      }
    }
  }
}

// ----------------------MINIMIZED ---------------------------------

.container-minimized {
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
      span,
      .despliega {
        opacity: 0;
      }
    }
  }
  .foot {
    .config {
      padding: 12px 20px;
      a {
        font-size: 1.2rem;
        span {
          margin-left: -200px;
        }
        .icono {
          display: block;
        }
      }
    }
    .profile {
      padding: 12px 12px;
      .user-profile {
        display: none;
      }
    }
  }
}
</style>