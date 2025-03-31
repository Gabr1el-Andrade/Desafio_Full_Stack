<template>
  <div id="app">
    <header class="navbar navbar-expand-lg">
      <a class="navbar-brand" href="#">Minha Loja</a>
      <ul class="navbar-nav">
        <li class="nav-item">
          <router-link class="nav-link" to="/produto/list">Lista de Produtos</router-link>
        </li>
        <li class="nav-item">
          <router-link class="nav-link" to="/products/new">Cadastrar Produto</router-link>
        </li>
        <li class="nav-item">
          <router-link class="nav-link" to="/categories/new">Cadastrar Categoria</router-link>
        </li>
      </ul>
    </header>
    <main class="container mt-4">
      <router-view />
    </main>
  </div>
</template>

<script setup>
</script>

<style scoped>
/* Estilo para o cabeçalho */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px 30px;
  background: linear-gradient(135deg, #007bff, #0056b3);
  color: #fff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.navbar-brand {
  font-size: 1.5rem;
  font-weight: bold;
  color: #fff;
  text-decoration: none;
  transition: color 0.3s ease;
}

.navbar-brand:hover {
  color: #d1ecf1;
}

.navbar-nav {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-item {
  margin-left: 20px;
}

.nav-link {
  font-size: 1rem;
  color: #fff;
  text-decoration: none;
  padding: 8px 15px;
  border-radius: 5px;
  transition: background-color 0.3s ease, color 0.3s ease;
}

.nav-link:hover {
  background-color: #0056b3;
  color: #d1ecf1;
}

.nav-link.router-link-active {
  background-color: #0056b3;
  color: #d1ecf1;
}

.container {
  margin-top: 20px;
}

@media (max-width: 768px) {
  .navbar {
    flex-direction: column;
    align-items: flex-start;
  }

  .navbar-nav {
    flex-direction: column;
    width: 100%;
  }

  .nav-item {
    margin-left: 0;
    margin-bottom: 10px;
  }

  .nav-link {
    width: 100%;
    text-align: left;
  }
}
</style>