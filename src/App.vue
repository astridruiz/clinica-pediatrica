<template>
  <div id="app">
 
    <header class="app-header">
      <nav class="nav-container">
        <router-link to="/" class="nav-link">Home</router-link>
        <router-link to="/login" class="nav-link">Login</router-link>
        <router-link to="/dashboard" class="nav-link">Dashboard</router-link>
      </nav>
    </header>

    <main class="app-main">
      <router-view />
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Londrina+Solid&display=swap');

#app {
  font-family: 'Londrina Solid', sans-serif;
  margin: 0;
  padding: 0;
}


.app-header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background: linear-gradient(90deg, #82c7ff, #c79bff, #ff9bdc);
  box-shadow: 0 4px 10px rgba(0,0,0,0.2);
  z-index: 100;
  padding: 15px 30px;
}


.nav-container {
  display: flex;
  justify-content: flex-end;
  gap: 20px;
}


.nav-link {
  color: white;
  font-weight: bold;
  text-decoration: none;
  padding: 8px 15px;
  border-radius: 20px;
  transition: all 0.3s ease;
}

.nav-link:hover {
  background-color: rgba(255,255,255,0.3);
  transform: translateY(-2px);
}


.app-main {
  padding-top: 80px; 
}
</style>