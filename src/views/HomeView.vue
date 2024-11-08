<template>
  <div class="container mt-5">
    <!-- Logo -->
    <div class="text-center">
      <img alt="Vue logo" src="../assets/logo.png" class="logo img-fluid mb-4" />
    </div>

    <!-- Título principal -->
    <h1 class="text-center text-primary font-weight-bold mb-4">Bienvenidos a la página de gestión de tareas con Vue</h1>

    <!-- Sección de contenido -->
    <div class="content">
      <h3 class="text-center text-info mb-3">Las opciones de esta página</h3>
      <p class="text-center text-muted mb-4">Añadir tarea: para agregar tareas y eliminarlas según sea necesario.</p>
      <p class="text-center text-muted mb-4">Lista de tareas: muestra de tareas determinadas.</p>
      <p class="text-center text-muted mb-4">Listas combinadas: permite agregar o eliminar tareas y visualizar las tareas predeterminadas.</p>

  
    </div>
  </div>
</template>

<style scoped>
/* Logo centrado y responsivo */
.logo {
  max-width: 150px;
  height: auto;
  box-shadow: 0 0 20px rgba(219, 67, 178, 0.71);
  transition: transform 0.3s,box-shadow 0.3s;
}
.logo:hover{
transform: scale(1.1);
box-shadow: 0 0 30px rgba(172, 22, 132, 0.92);
}
/* Estilos personalizados */
h1 {
  font-size: 2.5rem;
  letter-spacing: 1px;
  text-transform: uppercase;
}

h3 {
  font-size: 1.75rem;
  font-weight: 600;
}

.content {
  margin-top: 40px;
}

p {
  font-size: 1.2rem;
  line-height: 1.6;
  max-width: 800px;
  margin: 0 auto;
}

/* Efecto hover para el título */
h1:hover {
  color: #007bff;
}

/* Estilos responsivos con Bootstrap */
@media (max-width: 767px) {
  .logo {
    max-width: 100px;
  }

  h1 {
    font-size: 2rem;
  }

  h3 {
    font-size: 1.5rem;
  }
}
</style>
