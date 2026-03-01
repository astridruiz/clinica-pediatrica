<template>
  <div class="dashboard-container">

    <header class="dashboard-header">
      <h1>Mis Citas</h1>
      <button @click="nuevoModal = true">Nueva Cita</button>
    </header>


    <div class="cards-container">
      <div
        v-for="(cita,index) in citas"
        :key="index"
        class="card"
        :style="{ animationDelay: index*0.1 + 's' }"
      >
        <h2>{{ cita.nombre }}</h2>
        <p><strong>Hora:</strong> {{ cita.hora }}</p>
        <p>
          <strong>Consulta:</strong>
          <span :class="['badge', tipoColor(cita.tipo)]">{{ cita.tipo }}</span>
        </p>
        <button @click="abrirModal(cita)">Ver</button>
      </div>
    </div>

    
    <div v-if="modalVisible" class="modal-overlay" @click.self="cerrarModal">
      <div class="modal-card">
        <h2>Detalle de Cita</h2>
        <p><strong>Nombre:</strong> {{ selectedCita.nombre }}</p>
        <p><strong>Hora:</strong> {{ selectedCita.hora }}</p>
        <p><strong>Tipo de Consulta:</strong> {{ selectedCita.tipo }}</p>
        <button class="close-btn" @click="cerrarModal">Cerrar</button>
      </div>
    </div>

  
    <div v-if="nuevoModal" class="modal-overlay" @click.self="nuevoModal=false">
      <div class="modal-card">
        <h2>Nueva Cita</h2>
        <form @submit.prevent="agregarCita">
          <label>Nombre del Paciente</label>
          <input v-model="nuevaCita.nombre" type="text" placeholder="Ej: Juan Pérez" required />

          <label>Hora</label>
          <input v-model="nuevaCita.hora" type="time" required />

          <label>Tipo de Consulta</label>
          <select v-model="nuevaCita.tipo" required>
            <option disabled value="">Selecciona un tipo</option>
            <option>Consulta General</option>
            <option>Vacunación</option>
            <option>Control de Crecimiento</option>
          </select>

          <button type="submit" class="close-btn">Agregar</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DashboardView",
  data() {
    return {
      citas: [
        { nombre: "Juan Pérez", hora: "08:30", tipo: "Consulta General" },
        { nombre: "Ana Martínez", hora: "09:15", tipo: "Vacunación" },
        { nombre: "Luis Gómez", hora: "10:00", tipo: "Control de Crecimiento" },
      ],
      modalVisible: false,
      selectedCita: {},
      nuevoModal: false,
      nuevaCita: { nombre: "", hora: "", tipo: "" },
    };
  },
  methods: {
    abrirModal(cita) {
      this.selectedCita = cita;
      this.modalVisible = true;
    },
    cerrarModal() {
      this.modalVisible = false;
      this.selectedCita = {};
    },
    tipoColor(tipo) {
      switch (tipo) {
        case "Vacunación":
          return "badge-green";
        case "Consulta General":
          return "badge-blue";
        case "Control de Crecimiento":
          return "badge-orange";
        default:
          return "badge-gray";
      }
    },
    agregarCita() {
    
      this.citas.push({ ...this.nuevaCita });
      
      this.nuevaCita = { nombre: "", hora: "", tipo: "" };
      this.nuevoModal = false;
    },
  },
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Londrina+Solid&display=swap');

.dashboard-container {
  min-height: 100vh;
  padding: 20px;
  background: linear-gradient(135deg, #82c7ff, #c79bff, #ff9bdc);
  font-family: 'Londrina Solid', sans-serif;
}


.dashboard-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.dashboard-header h1 {
  color: white;
  font-size: 2rem;
  text-shadow: 2px 2px 5px rgba(0,0,0,0.3);
}

.dashboard-header button {
  padding: 10px 25px;
  border-radius: 25px;
  border: none;
  background-color: white;
  color: #6b21a8;
  font-weight: bold;
  cursor: pointer;
  box-shadow: 0 5px 15px rgba(0,0,0,0.2);
  transition: all 0.3s ease;
}

.dashboard-header button:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 20px rgba(0,0,0,0.3);
}


.cards-container {
  display: grid;
  grid-template-columns: repeat(auto-fill,minmax(250px,1fr));
  gap: 20px;
  max-height: calc(100vh - 100px);
  overflow-y: auto;
}

.card {
  background: white;
  border-radius: 25px;
  padding: 20px;
  box-shadow: 0 8px 20px rgba(0,0,0,0.2);
  transition: all 0.3s ease;
  animation: fadeUp 0.8s forwards;
  opacity: 0;
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 25px rgba(0,0,0,0.3);
}

.card h2 {
  color: #6b21a8;
  margin-bottom: 10px;
}

.card button {
  margin-top: 15px;
  padding: 8px 20px;
  border: none;
  border-radius: 20px;
  background-color: #6b21a8;
  color: white;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.3s ease;
}

.card button:hover {
  background-color: #7e2bb9;
  transform: translateY(-2px);
}


.badge {
  padding: 3px 10px;
  border-radius: 12px;
  color: white;
  font-weight: bold;
  font-size: 0.9rem;
}

.badge-green { background-color: #22c55e; }
.badge-blue { background-color: #3b82f6; }
.badge-orange { background-color: #f97316; }
.badge-gray { background-color: #6b7280; }


@keyframes fadeUp {
  from { opacity: 0; transform: translateY(20px);}
  to { opacity: 1; transform: translateY(0);}
}


.modal-overlay {
  position: fixed;
  top:0; left:0;
  width:100%; height:100%;
  background: rgba(0,0,0,0.5);
  display:flex;
  justify-content:center;
  align-items:center;
  z-index: 200;
  animation: fadeIn 0.3s;
}

.modal-card {
  background:white;
  padding:30px;
  border-radius:25px;
  width:90%;
  max-width:400px;
  box-shadow: 0 10px 25px rgba(0,0,0,0.3);
  text-align:center;
}

.modal-card h2 {
  color:#6b21a8;
  margin-bottom:15px;
}

.modal-card form {
  display:flex;
  flex-direction:column;
  gap:10px;
  text-align:left;
}

.modal-card form label {
  font-weight:bold;
}

.modal-card form input,
.modal-card form select {
  padding:10px;
  border-radius:15px;
  border:1px solid #ccc;
  outline:none;
}

.modal-card form input:focus,
.modal-card form select:focus {
  border-color: #6b21a8;
  box-shadow: 0 0 5px rgba(107,33,168,0.5);
}

.close-btn {
  margin-top:15px;
  padding:10px 25px;
  border:none;
  border-radius:25px;
  background-color:#6b21a8;
  color:white;
  font-weight:bold;
  cursor:pointer;
  transition: all 0.3s ease;
}

.close-btn:hover {
  background-color:#7e2bb9;
  transform: translateY(-2px);
}


@keyframes fadeIn {
  from { opacity:0;}
  to { opacity:1;}
}
</style>