<template>
  <div class="header">
    <ul class="nav-links">
      <li><router-link to="/" class="nav-link">Início</router-link></li>
      <li><router-link to="/Via-Cep" class="nav-link">Via Cep</router-link></li>
      <li><router-link to="/About" class="nav-link">Sobre</router-link></li>
    </ul>
    <router-view />
  </div>
</template>

<script setup>
// Se houver algum código JavaScript relacionado ao cabeçalho, pode ser adicionado aqui
</script>

<style scoped>
/* Estilos para o cabeçalho e links */
.header {
  padding: 15px;
}

.nav-links {
  list-style: none;
  display: flex;
  justify-content: space-around;
  padding: 0;
  margin: 0;
}

.nav-link {
  text-decoration: none;
  color: #333; /* Cor do texto dos links */
  padding: 8px 15px;
  border-radius: 4px;
}

.nav-link:hover {
  background-color: #f0f0f0; /* Cor de fundo ao passar o mouse */
}
</style>
