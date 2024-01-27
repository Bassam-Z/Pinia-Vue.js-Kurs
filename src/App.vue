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

        <!-- Loading -->
        <div v-if="isLoading" class="loading">
            Loading Tasks...
        </div>

        <!-- task list -->
        <div v-if="filter === 'all'" class="task-list">
            <p>You have {{ totalCount }} tasks left to do</p>
            <div v-for="task in tasks" :key="task.id">
                <TaskDetails :task="task"/>
            </div>
        </div>
        <div v-if="filter === 'favs'" class="task-list">
            <p>You have {{ favCount }} tasks left to do</p>
            <div v-for="task in favs" :key="task.id">
                <TaskDetails :task="task"/>
            </div>
        </div>
        <div class="filter">
            <button  @click="taskStore.$reset">reset State</button>
        </div>
    </main>
</template>

<script>
import TaskDetails from '@/components/TaskDetails.vue'
import { useTaskStore } from './stores/TasksStore'
import TaskForm from './components/TaskForm.vue'
import { ref } from 'vue'
import { storeToRefs } from 'pinia'
    export default {
        components: { TaskDetails, TaskForm },
        setup () {
            const taskStore = useTaskStore()

            const { tasks, isLoading, favs, totalCount, favCount } = storeToRefs(taskStore)

            // feth tasks
            taskStore.getTasks()

            const filter = ref('all')

            return { taskStore, filter,tasks, isLoading, favs, totalCount, favCount }
        }
    }
</script>


