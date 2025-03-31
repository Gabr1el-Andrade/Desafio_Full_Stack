<template>
    <div class="container mt-5">
      <div class="row justify-content-center">
        <div class="col-md-6">
          <div class="card shadow">
            <div class="card-header bg-primary text-white">
              <h4 class="mb-0">Cadastrar Categoria</h4>
            </div>
            <div class="card-body">
              <form @submit.prevent="submitForm">
                <div class="mb-3">
                  <label for="name" class="form-label">Nome da Categoria</label>
                  <input
                    type="text"
                    id="name"
                    class="form-control"
                    v-model="category.nome"
                    placeholder="Digite o nome da categoria"
                    required
                  />
                </div>
                <div class="text-end">
                  <button type="submit" class="btn btn-success">Cadastrar Categoria</button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue';
  import api from '@/api';
  
  const category = ref({ nome: '' });
  
  async function submitForm() {
    try {
      await api.post('/categorias', category.value, {
        headers: {
          Authorization: `Bearer ${localStorage.getItem('authToken')}`,
        },
      });
      alert('Categoria cadastrada com sucesso!');
      category.value.nome = ''; // Limpa o formulário
    } catch (error) {
      alert('Erro ao cadastrar categoria. Verifique os dados e tente novamente.');
      console.error(error);
    }
  }
  </script>
  
  <style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.card {
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  border: none;
  background-color: #f8f9fa;
}

.card-header {
  border-radius: 12px 12px 0 0;
  background: linear-gradient(135deg, #007bff, #0056b3);
  color: #fff;
  text-align: center;
  padding: 15px;
}

.card-body {
  padding: 25px;
}

.form-label {
  font-weight: bold;
  color: #495057;
}

.form-control {
  border-radius: 8px;
  border: 1px solid #ced4da;
  padding: 10px;
  font-size: 1rem;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
}

.form-control:focus {
  border-color: #007bff;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}

.btn-success {
  background-color: #28a745;
  border-color: #28a745;
  border-radius: 8px;
  padding: 10px 20px;
  font-size: 1rem;
  transition: background-color 0.3s ease, box-shadow 0.3s ease;
}

.btn-success:hover {
  background-color: #218838;
  box-shadow: 0 4px 8px rgba(40, 167, 69, 0.3);
}

.text-end {
  margin-top: 20px;
}

h4 {
  font-size: 1.5rem;
  font-weight: bold;
}

@media (max-width: 576px) {
  .container {
    padding: 10px;
  }

  .btn-success {
    width: 100%;
  }
}
</style>
  