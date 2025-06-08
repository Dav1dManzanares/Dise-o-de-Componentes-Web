<template>
  <div>
    <nav class="navbar">
      <div class="nav-left">Mi app - usuario</div>
      <button class="logout-btn" @click="logout"> cerrar secion</button>
    </nav>
  </div>

  <div class="container">
    <h1>usuario</h1>
    <button @click="showCreate = true">agregar usuario</button>

    <ul>
      <li v-for="user in users" :key="user._id">
        {{ user.email }}
        <button @click="ediUser(user)">editar</button>
        <button class="danger" @click="deleteUser(user)">Eliminar</button>
      </li>
    </ul>

    
  </div>

</template>

<script setup>
import { useAuthStore } from '../stores/auth'
import { useRouter } from 'vue-router'

const auth = useAuthStore()
const router = useRouter()

const cerrarSesion = () => {
  auth.logout()
  router.push('/login')
}
</script>

<style scoped>
.dashboard-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #e8f5e9;
}

.dashboard-content {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
  width: 100%;
  max-width: 400px;
}

.dashboard-content h1 {
  font-size: 28px;
  margin-bottom: 10px;
}

.dashboard-content p {
  color: #666;
  font-size: 16px;
  margin-bottom: 20px;
}

.logout-button {
  padding: 12px;
  background-color: #f44336;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

.logout-button:hover {
  background-color: #d32f2f;
}
</style>
