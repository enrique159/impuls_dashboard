<template>
  <div class="login-container">
    <div class="left-block">
      <div class="logo">
        <img src="@/assets/img/logo_black.png" alt="impuls">
        <h6 class="logo-title">Panel de control</h6>
      </div>

      <div class="user-credentials">
        <form id="login-form" @submit.prevent="login">
          <input type="text" id="username" class="username mb-3" placeholder="Nombre de usuario">
          <div class="user-password mb-4">
            <input type="password" id="password" class="password" placeholder="Contraseña">
            <div class="show-password">
              <img src="@/assets/icons/see-password.svg" alt="" class="eye">
            </div>
          </div>
          <button type="submit" class="signin-button mb-4">
            <img src="@/assets/icons/sign-in.svg" alt="">
            Ingresar al panel
          </button>
        </form>
        <div class="forget-password">
          <p>¿Has olvidado tu contraseña?</p>
          <a href="#">Haz click aquí</a>
        </div>
      </div>

      <div class="support-info d-flex flex-col">
        <p class="mb-1">Si no tienes una cuenta favor de <br>contactar al servicio de la plataforma.</p>
        <a href="#" class="mb-4">panel@impuls.com.mx</a>
        <button class="help-button">
          <img src="@/assets/icons/help.svg" alt="">
          Ayuda y Soporte
        </button>
      </div>
    </div>
    <!-- ////////////////// RIGHT COLUMN /////////////////// -->
    <div class="right-block">
      <div class="opacity-filter">
        <div class="terms-privacy d-flex">
          <a href="#">Términos y condiciones</a>
          <a href="#">Aviso de privacidad</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "LogIn",
  data() {
    return {
      username: "",
      password: "",
    }
  },
  methods: {
    login(e) {
      this.$router.push('/');
    },
  },
};
</script>

<style lang="scss" scoped>

</style>