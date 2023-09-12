<template>
    <header class="flex justify-between items-center my-5">
        <h1>To Do:</h1>
        <button
            @click="toggle"
            class="rounded-full bg-blue-800 p-2 px-4 text-white"
            >{{ showAddTask ? 'Close form' : 'Add Task' }}</button
        >
    </header>
</template>

<script>
export default {
    name: 'Header',
    props: {
        text: String,
        showAddTask: Boolean,
    },
    methods: {
        toggle() {
            this.$emit('toggle-add-task');
        },
    },
};
</script>
