<template>
  <div class="register-container">
    <h2>Registrar Usuário</h2>
    <form class="register-form" @submit.prevent="registerUser">
      <label>Nome:</label>
      <input v-model="name" type="text" placeholder="Digite seu nome" required />
      
      <label>Email:</label>
      <input v-model="email" type="email" placeholder="Digite seu email" required />
      
      <label>Senha:</label>
      <input v-model="password" type="password" placeholder="Digite sua senha" required />
      
      <label>Confirme a Senha:</label>
      <input
        v-model="passwordConfirmation"
        type="password"
        placeholder="Confirme sua senha"
        required
      />
      
      <button type="submit" class="register-button">Registrar</button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import { useRouter } from 'vue-router';
import api from '@/api';

export default defineComponent({
  setup() {
    const name = ref('');
    const email = ref('');
    const password = ref('');
    const passwordConfirmation = ref('');
    const router = useRouter();

    const registerUser = async () => {
      try {
        await api.post('/register', {
          name: name.value,
          email: email.value,
          password: password.value,
          password_confirmation: passwordConfirmation.value,
        });
        alert('Usuário registrado com sucesso!');
        router.push('/'); // Redireciona para a tela de login
      } catch (error) {
        console.error(error);
      }
    };

    return { name, email, password, passwordConfirmation, registerUser };
  },
});
</script>

<style scoped>
.register-container {
  max-width: 450px;
  margin: 50px auto;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.1);
  background: linear-gradient(135deg, #f8f9fa, #e9ecef);
}

h2 {
  text-align: center;
  margin-bottom: 25px;
  color: #333;
  font-size: 1.8rem;
  font-weight: bold;
}

.register-form {
  display: flex;
  flex-direction: column;
}

.register-form label {
  margin-bottom: 8px;
  font-weight: bold;
  color: #555;
}

.register-form input {
  padding: 12px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 1rem;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
}

.register-form input:focus {
  border-color: #007bff;
  outline: none;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}

.register-button {
  padding: 12px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s ease, box-shadow 0.3s ease;
}

.register-button:hover {
  background-color: #0056b3;
  box-shadow: 0 4px 8px rgba(0, 91, 179, 0.3);
}

.register-button:focus {
  outline: none;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}

@media (max-width: 768px) {
  .register-container {
    padding: 20px;
  }

  h2 {
    font-size: 1.5rem;
  }

  .register-form input {
    font-size: 0.9rem;
    padding: 10px;
  }

  .register-button {
    font-size: 0.9rem;
    padding: 10px;
  }
}
</style>