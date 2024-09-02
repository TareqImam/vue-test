<script>
export default {
    data() {
        return {
            name: 'Imam',
            status: 'inactive',
            tasks: ['One', 'Two', 'Three'],
            link: 'https://google.com',
        };
    },
    methods: {
        toggleStatus() {
            console.log(this.status);

            if (this.status === 'active') {
                this.status = 'pending';
            } else if (this.status === 'pending') {
                this.status = 'inactive';
            } else {
                this.status = 'active';
            }
        },
    },
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

    <!-- <a v-bind:href="link">Click For Google</a> -->
    <!-- <br /> -->
    <a :href="link" target="_blank">Click For Google</a>
    <br />

    <!-- <button v-on:click="toggleStatus">Change Status</button> -->
    <button @click="toggleStatus">Change Status</button>
</template>
