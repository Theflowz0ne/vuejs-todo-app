<template>
    <div class="container m-auto max-w-lg px-5 py-2 mt-10 rounded-xl shadow-xl">
        <Header
            @toggle-add-task="toggle"
            text="Add"
            :showAddTask="showAddTask" />
        <AddTask
            :class="[showAddTask ? 'block' : 'hidden']"
            @add-task="addTask" />
        <Tasks
            @toggle-reminder="toggleReminder"
            @delete-task="deleteTask"
            :tasks="tasks" />
    </div>
</template>

<script>
import Header from './components/Header.vue';
import Tasks from './components/Tasks.vue';
import AddTask from './components/AddTask.vue';

export default {
    name: 'App',
    components: {
        Header,
        Tasks,
        AddTask,
    },
    data() {
        return {
            tasks: [],
            showAddTask: false,
        };
    },
    methods: {
        async deleteTask(id) {
            if (confirm(`You are about to delete a task! Are you sure?`)) {
                const res = await fetch(`/api/tasks/${id}`, {
                    method: 'DELETE',
                });

                res.status === 200
                    ? (this.tasks = this.tasks.filter((task) => task.id !== id))
                    : alert('Error deleting task');
            }
        },
        async toggleReminder(id) {
            const taskToToggle = await this.fetchTask(id);
            const updTask = {
                ...taskToToggle,
                reminder: !taskToToggle.reminder,
            };

            const res = await fetch(`api/tasks/${id}`, {
                method: 'PUT',
                headers: {
                    'Content-type': 'application/json',
                },
                body: JSON.stringify(updTask),
            });

            const data = await res.json();

            this.tasks = this.tasks.map((task) =>
                task.id === id ? { ...task, reminder: data.reminder } : task,
            );
        },
        async addTask(newTask) {
            const res = await fetch('api/tasks', {
                method: 'POST',
                headers: {
                    'Content-type': 'application/json',
                },
                body: JSON.stringify(newTask),
            });

            const data = await res.json();
            this.tasks = [...this.tasks, data];
        },
        toggle() {
            this.showAddTask = !this.showAddTask;
        },
        async fetchTasks() {
            const res = await fetch('api/tasks');
            const data = await res.json();
            return data;
        },
        async fetchTask(id) {
            const res = await fetch(`api/tasks/${id}`);
            const data = await res.json();
            return data;
        },
    },
    async created() {
        this.tasks = await this.fetchTasks();
    },
};
</script>

<style scoped></style>
