<template>
    <form
        class="mb-3"
        @submit="onSubmit">
        <!-- Text Input -->
        <div class="mb-4">
            <label
                for="text-input"
                class="block text-gray-700 font-bold"
                >Task Name</label
            >
            <input
                type="text"
                v-model="text"
                id="text-input"
                name="text-input"
                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring focus:border-blue-300"
                placeholder="Enter your task name" />
        </div>

        <!-- Date & Time Input -->
        <div class="mb-4">
            <label
                for="date-picker"
                class="block text-gray-700 font-bold"
                >Date & Time</label
            >
            <input
                type="text"
                v-model="day"
                id="date-picker"
                name="date-picker"
                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring focus:border-blue-300"
                placeholder="Choose a date & time" />
        </div>
        <div class="mb-4 flex">
            <input
                type="checkbox"
                v-model="reminder"
                id="task-reminder"
                name="task-reminder"
                class="rounded-lg w-5 mr-5" />
            <label
                for="task-reminder"
                class="text-gray-700 font-bold"
                >Set Reminder</label
            >
        </div>
        <button
            type="submit"
            @:click="onClick"
            class="rounded-full bg-blue-800 p-2 px-4 text-white"
            >Save Task</button
        ></form
    ></template
>
<script>
export default {
    name: 'AddTask',
    data() {
        return {
            text: '',
            day: '',
            reminder: false,
        };
    },
    methods: {
        onSubmit(e) {
            e.preventDefault();

            if (!this.text) {
                alert(`You haven't added a task`);
                return;
            }

            const newTask = {
                text: this.text,
                day: this.day,
                reminder: this.reminder,
            };

            this.$emit('add-task', newTask);

            this.text = '';
            this.day = '';
            this.reminder = false;
        },
    },
};
</script>
