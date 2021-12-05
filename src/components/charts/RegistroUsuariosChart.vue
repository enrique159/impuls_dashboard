<template>
  <div class="container">
    <div class="header">
      <div class="title">
        <span>Registro de usuarios</span>
      </div>
      <DropdownButtonWhite />
    </div>
    <table class="usuarios">
      <tr>
        <td>Usuarios totales</td>
        <td class="total">{{ usuariosTotales }}</td>
      </tr>
      <tr>
        <td>Nuevos en el mes</td>
        <td>{{ usuariosNuevos }}</td>
      </tr>
      <tr>
        <td>Inactivos por 7 dias</td>
        <td>{{ usuariosInactivos }}</td>
      </tr>
      <tr>
        <td>% Crecimiento</td>
        <td class="crecimiento">
          <div class="arrow-up"></div>
          {{ crecimiento }}
        </td>
      </tr>
    </table>
    <button class="user-button">
      <span>Ver usuarios</span>
      <i class="ri-arrow-right-line ml-2"></i>
    </button>
  </div>
</template>

<script>
import DropdownButtonWhite from "@/components/DropdownButtonWhite.vue";
export default {
  name: "RegistroUsuariosChart",
  components: {
    DropdownButtonWhite,
  },
  data() {
    return {
      usuariosTotales: 59,
      usuariosNuevos: 10,
      usuariosInactivos: 5,
      crecimiento: 0.98,
    };
  },
};
</script>

<style lang="scss" scoped>
.container {
  width: 49%;
  margin-top: 48px;
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
  // USUARIOS ////////////////////
  .usuarios {
    width: 100%;
    margin-top: 24px;
    border-collapse: collapse;
    border-spacing: 0;
    font-size: 1.1rem;
    color: #000000;
    tr {
      height: 42px;
      td {
        padding: 0 24px;
        &:first-child {
          width: 80%;
        }
        &:last-child {
          text-align: right;
          font-size: 1.3rem;
          font-weight: 600;
          width: 20%;
        }
      }
      .crecimiento {
        display: flex;
        justify-content: flex-start;
        align-items: center;
        height: 42px;
        .arrow-up {
          width: 0;
          height: 0;
          border-left: 5px solid transparent;
          border-right: 5px solid transparent;
          border-bottom: 5px solid rgb(226, 27, 93);
          transform: rotate(180deg);
          margin-right: 4px;
        }
      }
      .total {
        font-size: 1.5rem !important;
        font-weight: 800 !important;
      }
    }
  }
  // USER BUTTON ////////////////////
  .user-button {
    transition: 0.2s ease-in-out;
    width: fit-content;
    margin-left: 24px;
    margin-top: 24px;
    height: fit-content;
    background: none;
    border: none;
    cursor: pointer;
    font-size: 1.1rem;
    font-weight: 800;
    display: flex;
    align-items: flex-end;
    &:hover {
      opacity: 0.6;
    }
  }
}
</style>