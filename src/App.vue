<template>
    <main>
        <!-- heading -->
        <header>
            <img src="./assets//pinia-logo.svg" alt="pinia logo">
            <h1>Pinia Tasks</h1>
        </header>

        <!-- new Task Form -->
        <div class="new-task-form">
            <TaskForm/>
        </div>

        <!-- filter -->
        <nav class="filter">
            <button @click="filter = 'all'">All tasks</button>
            <button @click="filter = 'favs'">Fav tasks</button>
        </nav>

        <!-- task list -->
        <div v-if="filter === 'all'" class="task-list">
            <p>You have {{ taskStore.totalCount }} tasks left to do</p>
            <div v-for="task in taskStore.tasks" :key="task.id">
                <TaskDetails :task="task"/>
            </div>
        </div>
        <div v-if="filter === 'favs'" class="task-list">
            <p>You have {{ taskStore.favCount }} tasks left to do</p>
            <div v-for="task in taskStore.favs" :key="task.id">
                <TaskDetails :task="task"/>
            </div>
        </div>
    </main>
</template>

<script>
import TaskDetails from '@/components/TaskDetails.vue'
import { useTaskStore } from './stores/TasksStore'
import TaskForm from './components/TaskForm.vue'
import { ref } from 'vue'
    export default {
        components: { TaskDetails, TaskForm },
        setup () {
            const taskStore = useTaskStore()
            const filter = ref('all')

            return { taskStore, filter }
        }
    }
</script>


