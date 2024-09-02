<script setup>
import { ref } from 'vue';

const name = ref('Imam');
const status = ref('active');
const tasks = ref(['One', 'Two', 'Three']);

const toggleStatus = () => {
    if (status.value === 'active') {
        status.value = 'pending';
    } else if (status.value === 'pending') {
        status.value = 'inactive';
    } else {
        status.value = 'active';
    }
};
</script>

<template>
    <h1>{{ name }}</h1>
    <br />
    <p v-if="status === 'active'">User Active</p>
    <p v-else-if="status === 'pending'">User Pending</p>
    <p v-else>User Inactive</p>
    <br />

    <h3>
        Tasks:
        <ul>
            <li v-for="task in tasks" :key="task">{{ task }}</li>
        </ul>
    </h3>
    <br />

    <button @click="toggleStatus">Change Status</button>
</template>
