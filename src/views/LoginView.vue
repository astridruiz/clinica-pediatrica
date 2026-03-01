<template>
  <div class="login-container">
    <div class="login-card">
      <h2 class="login-title">Iniciar Sesión</h2>
      <form @submit.prevent="login">
        <label>Usuario</label>
        <input v-model="username" type="text" placeholder="Ingresa tu usuario" />

        <label>Contraseña</label>
        <input v-model="password" type="password" placeholder="Ingresa tu contraseña" />

        <button type="submit">Entrar</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "LoginView",
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    login() {
      this.$router.push("/dashboard");
    },
  },
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Londrina+Solid&display=swap');

.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: linear-gradient(135deg, #c79bff, #82c7ff, #ff9bdc);
  font-family: 'Londrina Solid', sans-serif;
}

.login-card {
  background: white;
  padding: 40px;
  border-radius: 30px;
  box-shadow: 0 10px 25px rgba(0,0,0,0.2);
  width: 100%;
  max-width: 400px;
  animation: fadeIn 0.8s ease;
}

.login-title {
  text-align: center;
  color: #6b21a8;
  font-size: 2rem;
  margin-bottom: 20px;
}

form label {
  display: block;
  margin-top: 15px;
  margin-bottom: 5px;
  font-weight: bold;
}

form input {
  width: 100%;
  padding: 12px;
  border-radius: 15px;
  border: 1px solid #ccc;
  outline: none;
  transition: all 0.3s ease;
}

form input:focus {
  border-color: #6b21a8;
  box-shadow: 0 0 5px rgba(107,33,168,0.5);
}

form button {
  width: 100%;
  padding: 15px;
  background-color: #6b21a8;
  color: white;
  font-weight: bold;
  border: none;
  border-radius: 25px;
  margin-top: 20px;
  cursor: pointer;
  transition: all 0.3s ease;
}

form button:hover {
  background-color: #7e2bb9;
  transform: translateY(-3px);
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(-20px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>