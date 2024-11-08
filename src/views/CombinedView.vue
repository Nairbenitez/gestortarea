<template>
    <div class="task-container">
        <!-- Sección para agregar nuevas tareas -->
        <div class="add-task-container">
            <h1>Añadir Tarea</h1>
            <div class="input-group">
                <input 
                    v-model="newTask" 
                    @keyup.enter="addTask" 
                    placeholder="Añadir nueva tarea" 
                    class="task-input"
                />
                <button @click="addTask" class="add-button">Añadir</button>
            </div>
        </div>

        <!-- Sección para mostrar y gestionar la lista de tareas -->
        <div v-if="tasks.length > 0" class="task-list">
            <h1>Lista de Tareas</h1>
            <div v-for="task in tasks" :key="task.id" class="task-item">
                <span :class="{ completed: task.completed }">{{ task.todo }}</span>
                <div>
                    <button @click="toggleTaskCompletion(task)">
                        <svg class="w-6 h-6 text-gray-800 dark:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
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

        <div v-else>
            <p>No hay tareas para mostrar.</p>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "TaskApp",
    data() {
        return {
            newTask: "", // Campo de entrada para la nueva tarea
            tasks: [],   // Lista de tareas (local y/o obtenidas de la API)
        };
    },
    methods: {
        // Agregar una tarea nueva
        addTask() {
            if (this.newTask.trim() === "") return;

            const newTask = {
                todo: this.newTask,
                completed: false,
                id: Date.now(), // Usamos el timestamp como ID único
            };

            // Añadir la nueva tarea a la lista
            this.tasks.unshift(newTask);
            this.newTask = ""; // Limpiar el campo de entrada
        },

        // Eliminar una tarea específica de la lista
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },

        // Cambiar el estado de la tarea entre completada y no completada
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },

        // Cargar tareas desde una API externa (si es necesario)
        async fetchTasks() {
            try {
                const response = await axios.get('https://dummyjson.com/todos');
                this.tasks = response.data.todos;
            } catch (error) {
                console.error("Error al cargar las tareas:", error);
                alert("Ocurrió un error al cargar las tareas.");
            }
        }
    },

    created() {
        // Cargar tareas automáticamente al iniciar el componente
        this.fetchTasks();
    },
};
</script>

<style scoped>
.task-container {
    padding: 20px;
    max-width: 600px;
    margin: 0 auto;
}

.add-task-container {
    margin-bottom: 30px;
}

.input-group {
    display: flex;
    margin-bottom: 10px;
}

.task-input {
    flex-grow: 1;
    padding: 8px;
    margin-right: 5px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

.add-button {
    padding: 8px 12px;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: white;
    cursor: pointer;
}

.add-button:hover {
    background-color: #0056b3;
}

.task-list {
    margin-top: 20px;
}

.task-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    border-bottom: 1px solid #eee;
}

.completed {
    text-decoration: line-through;
    color: gray;
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

h1 {
    color: #333;
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
