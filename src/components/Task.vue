<template>
    <div
        @dblclick="$emit('toggle-reminder', task.id)"
        :class="[
            task.reminder ? 'border-l-green-800' : '',
            'bg-blue-200 my-1 px-4 py-1 border-2 border-gray-300 rounded-full shadow-lg',
        ]">
        <h2 class="text-lg flex flex-row justify-between"
            >{{ task.text }}
            <i
                @click="onDelete(task.id)"
                class="fas fa-times text-red-600 pt-1 pr-1"></i
        ></h2>
        <p class="text-sm">{{ task.day }}</p>
    </div>
</template>

<script>
export default {
    name: 'Task',
    props: {
        task: Object,
    },
    methods: {
        onDelete(id) {
            this.$emit('delete-task', id);
        },
    },
};
</script>
