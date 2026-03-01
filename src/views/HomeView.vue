<template>
  <div class="home-container">
    <h1 class="title">Clínica Pediátrica Familiar</h1>
    <p class="subtitle">
      Bienvenido al sistema de citas pediátricas. Agenda tus consultas de forma rápida y segura.
    </p>
    <router-link to="/login" class="btn-primary">Iniciar Sesión</router-link>
  </div>
</template>

<script>
export default { name: "HomeView" }
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Londrina+Solid&display=swap');

.home-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  padding: 20px;
  background: linear-gradient(135deg, #82c7ff, #c79bff, #ff9bdc);
  text-align: center;
  font-family: 'Londrina Solid', sans-serif;
}

.title {
  font-size: 4rem;
  color: white;
  margin-bottom: 20px;
  text-shadow: 2px 2px 5px rgba(0,0,0,0.3);
}

.subtitle {
  color: white;
  font-size: 1.2rem;
  max-width: 500px;
  margin-bottom: 30px;
  text-shadow: 1px 1px 4px rgba(0,0,0,0.3);
}

.btn-primary {
  padding: 15px 40px;
  background-color: white;
  color: #6b21a8;
  font-weight: bold;
  border-radius: 25px;
  text-decoration: none;
  box-shadow: 0 5px 15px rgba(0,0,0,0.2);
  transition: all 0.3s ease;
}

.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 20px rgba(0,0,0,0.3);
}
</style>