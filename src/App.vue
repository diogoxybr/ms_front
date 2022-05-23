<template>
  <div id="app">

<b-navbar toggleable="lg" type="dark" variant="info" v-if="notIsLoginPage">
    <a class="navbar-brand" href="/">
        <img id="logo" alt="Logo" src="../src/assets/logo.png" height="32" />
    </a>
    <b-navbar-brand href="/">Magic Seed</b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
        <b-nav-item to="/">Início</b-nav-item>
        <b-nav-item to="/form">Novo plantio</b-nav-item>
        <b-nav-item to="/plants">Plantas</b-nav-item>
        <b-nav-item to="/guide">Guia de cultivo</b-nav-item>
        <b-nav-item to="/shop">Loja</b-nav-item>
        <b-nav-item to="/about">Sobre</b-nav-item>
      </b-navbar-nav>

      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
        <b-nav-item-dropdown right>
          <!-- Using 'button-content' slot -->
          <template #button-content>
            <em>Usuário</em>
          </template>
          <b-dropdown-item to="/register">Alterar cadastro</b-dropdown-item>
          <b-dropdown-item to="/login">Sair</b-dropdown-item>
        </b-nav-item-dropdown>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
  
  <transition name="fade" mode="out-in">
    <router-view />
  </transition>
  </div>
</template>

<script>
export default {
  computed: {
    notIsLoginPage() {
      return this.$route.name !== "login" && this.$route.name !== "register";
    }
  }
}
</script>

<style>
.fade-enter-active, .fade-leave-active {
  transition-duration: 0.5s;
  transition-property: opacity;
  transition-timing-function: ease;
}

.fade-enter, .fade-leave {
  opacity: 0;
}
</style>
