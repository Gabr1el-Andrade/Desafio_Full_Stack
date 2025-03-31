<template>
  <div class="container mt-5">
    <div class="row justify-content-center">
      <div class="col-md-8">
        <div class="card shadow">
          <div class="card-header bg-primary text-white">
            <h4 class="mb-0">{{ isEditing ? 'Editar Produto' : 'Cadastrar Produto' }}</h4>
          </div>
          <div class="card-body">
            <form @submit.prevent="submitForm">
              <div class="mb-3">
                <label for="nome" class="form-label">Nome do Produto</label>
                <input
                  type="text"
                  id="nome"
                  class="form-control"
                  v-model="product.nome"
                  placeholder="Digite o nome do produto"
                  required
                />
              </div>
              <div class="mb-3">
                <label for="descricao" class="form-label">Descrição</label>
                <textarea
                  id="descricao"
                  class="form-control"
                  v-model="product.descricao"
                  placeholder="Digite a descrição do produto"
                  required
                ></textarea>
              </div>
              <div class="mb-3">
                <label for="preco" class="form-label">Preço</label>
                <input
                  type="number"
                  id="preco"
                  class="form-control"
                  v-model="product.preco"
                  min="0"
                  step="0.01"
                  placeholder="Digite o preço do produto"
                  required
                />
              </div>
              <div class="mb-3">
                <label for="data_validade" class="form-label">Data de Validade</label>
                <input
                  type="date"
                  id="data_validade"
                  class="form-control"
                  v-model="product.data_validade"
                  required
                />
              </div>
              <div class="mb-3">
                <label for="imagem" class="form-label">Imagem</label>
                <input
                  type="file"
                  id="imagem"
                  class="form-control"
                  @change="handleImageUpload"
                />
              </div>
              <div class="mb-3">
                <label for="categoria_id" class="form-label">Categoria ID</label>
                <input
                  type="number"
                  id="categoria_id"
                  class="form-control"
                  v-model="product.categoria_id"
                  min="1"
                  required
                />
              </div>
              <div class="text-end">
                <button type="submit" class="btn btn-success">
                  {{ isEditing ? 'Salvar Alterações' : 'Cadastrar Produto' }}
                </button>
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
import { createProduct, updateProduct } from "@/service/productService";
import type { Produto } from '@/service/productService';

// Emissão de eventos para o componente pai
const emit = defineEmits(['produtoAdicionado']);

const product = ref<Partial<Produto>>({
  nome: '',
  descricao: '',
  preco: 0,
  data_validade: '',
  imagem: '',
  categoria_id: 0,
});

const isEditing = ref(false);
const productId = ref<number | null>(null); // Usado para edição, se necessário

function handleImageUpload(event: Event) {
  const file = (event.target as HTMLInputElement).files?.[0];
  if (file && file.type.startsWith('image/')) {
    product.value.imagem = file;
  } else {
    alert('Por favor, selecione um arquivo de imagem válido.');
  }
}

async function submitForm() {
  try {
    const formData = new FormData();
    Object.entries(product.value).forEach(([key, value]) => {
      if (value !== null && value !== undefined) {
        formData.append(key, value instanceof File ? value : String(value));
      }
    });

    if (isEditing.value && productId.value !== null) {
      await updateProduct(productId.value, formData);
      alert('Produto atualizado com sucesso!');
    } else {
      await createProduct(formData);
      alert('Produto cadastrado com sucesso!');
    }

    // Emitir evento para o componente pai
    emit('produtoAdicionado');

    // Limpar o formulário
    product.value = {
      nome: '',
      descricao: '',
      preco: 0,
      data_validade: '',
      imagem: '',
      categoria_id: 0,
    };
    isEditing.value = false;
    productId.value = null;
  } catch (error) {
    alert('Erro ao salvar o produto. Verifique os dados e tente novamente.');
    console.error(error);
  }
}
</script>

<style scoped>
.container {
  max-width: 900px;
  margin: 50px auto;
  padding: 20px;
}

.card {
  border-radius: 12px;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.1);
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
  padding: 30px;
}

h4 {
  font-size: 1.8rem;
  font-weight: bold;
}

.form-label {
  font-weight: bold;
  color: #495057;
}

.form-control {
  border-radius: 8px;
  border: 1px solid #ced4da;
  padding: 12px;
  font-size: 1rem;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
}

.form-control:focus {
  border-color: #007bff;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}

textarea.form-control {
  resize: none;
}

.btn-success {
  background-color: #28a745;
  border-color: #28a745;
  border-radius: 8px;
  padding: 12px 20px;
  font-size: 1rem;
  font-weight: bold;
  transition: background-color 0.3s ease, box-shadow 0.3s ease;
}

.btn-success:hover {
  background-color: #218838;
  box-shadow: 0 4px 8px rgba(40, 167, 69, 0.3);
}

.text-end {
  margin-top: 20px;
}

input[type="file"] {
  padding: 5px;
}

@media (max-width: 768px) {
  .container {
    padding: 10px;
  }

  .card-body {
    padding: 20px;
  }

  .btn-success {
    width: 100%;
  }
}
</style>
