<script setup>
import { onMounted, ref } from 'vue';

const name = ref('Imam');
const status = ref('active');
const tasks = ref(['One', 'Two', 'Three']);
const newTask = ref('');

const toggleStatus = () => {
    if (status.value === 'active') {
        status.value = 'pending';
    } else if (status.value === 'pending') {
        status.value = 'inactive';
    } else {
        status.value = 'active';
    }
};

const addTask = () => {
    if (newTask.value.trim() !== '') {
        tasks.value.push(newTask.value);
        newTask.value = '';
    }
};

const deleteTask = (index) => {
    tasks.value.splice(index, 1);
};

onMounted(async () => {
    try {
        const response = await fetch(
            'https://jsonplaceholder.typicode.com/todos'
        );
        const data = await response.json();
        tasks.value = data.map((task) => task.title);
    } catch (error) {
        console.log(error);
    }
});
</script>

<template>
    <h1>{{ name }}</h1>
    <br />
    <p v-if="status === 'active'">User Active</p>
    <p v-else-if="status === 'pending'">User Pending</p>
    <p v-else>User Inactive</p>
    <br />

    <form @submit.prevent="addTask">
        <label for="newTask">Add Task</label>
        <br />
        <input type="text" id="newTask" name="newTask" v-model="newTask" />
        <button type="submit">Submit</button>
    </form>
    <br />

    <h3>
        Tasks:
        <ul>
            <li v-for="(task, index) in tasks" :key="task">
                <span>{{ task }}</span>
                <button @click="deleteTask(index)">X</button>
            </li>
        </ul>
    </h3>
    <br />

    <button @click="toggleStatus">Change Status</button>
</template>
