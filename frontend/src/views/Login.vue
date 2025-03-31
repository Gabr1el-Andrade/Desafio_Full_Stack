<template>
    <div class="login-container">
      <h2>Login</h2>
      <form class="login-form" @submit.prevent="loginUser">
        <label>Email:</label>
        <input v-model="email" type="email" placeholder="Digite seu email" required />
        
        <label>Senha:</label>
        <input v-model="password" type="password" placeholder="Digite sua senha" required />
        
        <button type="submit" class="login-button">Login</button>
      </form>
      <div class="redirect-container">
        <p>Não possui uma conta?</p>
        <button class="register-button" @click="goToRegister">Registrar-se</button>
      </div>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent, ref } from 'vue';
  import { useRouter } from 'vue-router';
  import api from '@/api';
  import { TokenService } from '@/service/TokenService';
  
  export default defineComponent({
    setup() {
      const email = ref('');
      const password = ref('');
      const router = useRouter();
  
      const loginUser = async () => {
        try {
          const response = await api.post('/login', {
            email: email.value,
            password: password.value,
          });
          TokenService.saveToken(response.data.token);
          alert('Login realizado com sucesso!');
          router.push('/produto/list'); // Redireciona para a tela da lista de produtos
        } catch (error) {
          console.error(error);
        }
      };
  
      const goToRegister = () => {
        router.push('/register'); // Redireciona para a página de registro
      };
  
      return { email, password, loginUser, goToRegister };
    },
  });
  </script>
  
 <style scoped>
.login-container {
  max-width: 400px;
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

.login-form {
  display: flex;
  flex-direction: column;
}

.login-form label {
  margin-bottom: 8px;
  font-weight: bold;
  color: #555;
}

.login-form input {
  padding: 12px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 1rem;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
}

.login-form input:focus {
  border-color: #007bff;
  outline: none;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}

.login-button {
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

.login-button:hover {
  background-color: #0056b3;
  box-shadow: 0 4px 8px rgba(0, 91, 179, 0.3);
}

.login-button:focus {
  outline: none;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}

.redirect-container {
  text-align: center;
  margin-top: 25px;
}

.redirect-container p {
  margin-bottom: 10px;
  color: #555;
  font-size: 0.9rem;
}

.register-button {
  padding: 10px 15px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 0.9rem;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s ease, box-shadow 0.3s ease;
}

.register-button:hover {
  background-color: #218838;
  box-shadow: 0 4px 8px rgba(40, 167, 69, 0.3);
}

.register-button:focus {
  outline: none;
  box-shadow: 0 0 5px rgba(40, 167, 69, 0.5);
}
</style>
  