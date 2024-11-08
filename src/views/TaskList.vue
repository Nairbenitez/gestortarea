<template>
    <div class="container mt-4">
        <h1 class="text-center mb-4 title aling-item-center">Lista de Tareas</h1>
        <div class="text-center mb-3">
            <button @click="fetchTasks"> <svg class="w-6 h-6 text-gray-800 dark:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
                <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 15v2a3 3 0 0 0 3 3h10a3 3 0 0 0 3-3v-2m-8 1V4m0 12-4-4m4 4 4-4"/>
                </svg>Cargar Tareas</button>
                <div v-if="tasks.length > 0">
                    <div v-for="task in tasks" :key="task.id">
                        <div>
                            <h5 :style="{ textDecoration: task.completed ? 'line-through' : 'none' }">{{ task.todo }}</h5>
                            <span>{{ task.completed ? 'Completada' : 'Pendiente' }}</span>
                            <button @click="toggleTaskCompletion(task)"><svg class="w-6 h-6 text-gray-800 dark:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
                            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.5 11.5 11 14l4-4m6 2a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z"/>
                            </svg>
                            </button>
                            <button @click="deleteTask(task)"><svg class="w-6 h-6 text-gray-800 dark:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
                            <path stroke="currentColor" stroke-linecap="round" stroke-width="2" d="m6 6 12 12m3-6a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z"/>
                            </svg>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "TaskList",
    data() {
        return {
            tasks: [], // Almacenamiento local de las tareas traídas de la API
        };
    },
    methods: {
        // Llamada para obtener las tareas desde la API externa
        async fetchTasks() {
            try {
                // Realiza la solicitud a la API
                const response = await axios.get('https://dummyjson.com/todos');
                // Asigna las tareas recibidas a la propiedad 'tasks'
                this.tasks = response.data.todos;
            } catch (error) {
                console.error("Error al cargar las tareas:", error);
                alert("Ocurrió un error al cargar las tareas.");
            }
        },

        // Cambiar el estado de una tarea (completada/no completada)
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },

        // Eliminar la tarea seleccionada
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);/* estlint-disable */
        },
    },
};
</script>

<style scoped>
/* Estilos básicos */
h1 {
    color: #333;
}
.container{
padding: 20px;
    max-width: 600px;
    margin: 0 auto;
}
button {
    margin: 5px;
    padding: 8px 15px;
    background-color: #5cb85c;
    color: white;
    border: none;
    border-radius: 3px;
    cursor: pointer;
}

button:hover {
    background-color: #4cae4c;
}

h5 {
    font-size: 1.2em;
    margin: 10px 0;
}

div {
    margin: 10px 0;
}

span {
    font-weight: bold;
}

p {
    color: #888;
}
</style>
