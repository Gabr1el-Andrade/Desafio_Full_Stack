<template>
  <div class="protected-container">
    <div class="content">
      <h1>Bem-vindo à Rota Protegida</h1>
      <p>Você só pode acessar esta página porque está autenticado.</p>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'ProtectedView',
});
</script>

<style scoped>
.protected-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: linear-gradient(135deg, #4caf50, #81c784);
  color: #fff;
  text-align: center;
}

.content {
  background: rgba(255, 255, 255, 0.1);
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
  max-width: 600px;
}

h1 {
  font-size: 2.5rem;
  font-weight: bold;
  margin-bottom: 20px;
  color: #fff;
}

p {
  font-size: 1.2rem;
  line-height: 1.6;
  color: #f1f1f1;
}

@media (max-width: 768px) {
  h1 {
    font-size: 2rem;
  }

  p {
    font-size: 1rem;
  }

  .content {
    padding: 20px;
  }
}
</style>