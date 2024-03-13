<template>
    <Navigation />
    <div class="p-8">
        <div class="bg-[#3498db] w-3/4 md:w-1/2 m-auto p-6 rounded-lg shadow-md">
    <h1 class="text-center text-2xl font-bold text-white mb-4">Add Your Task</h1>
    <div class="mb-4">
        <input type="text" v-model="tasks.newTask" placeholder="Enter your task here..."
            class="w-full px-4 py-2 rounded-md border border-white text-gray-800 focus:outline-none focus:border-[#2c3e50]"
            required>
    </div>
    <button type="button" v-on:click="newTask"
        class="w-full bg-[#2ecc71] px-4 py-2 rounded-md text-white hover:bg-[#27ae60] focus:outline-none focus:bg-[#27ae60]">
        ADD NEW TASK
    </button>
</div>

    </div>
</template>
<script>
import Navigation from './Navigation.vue';
import axios from 'axios';

export default {
    name: 'AddTask',
    components: {
        Navigation
    },
    data() {
        return {
            tasks: {
                newTask: '',
                date: '',
                status: 'Not Completed'
            }
        }
    },
    methods: {
        async newTask() {
            let result = await axios.post('http://localhost:3000/tasks', {
                newTask: this.tasks.newTask.trim(),
                date: this.tasks.date,
                status: this.tasks.status
            })
            console.log('Task added...', result);

            if (result.status == 201) {
                alert("Task added");
                this.$router.push({ name: 'ShowTask' });
            }
        },
        getCurrentDate() {
            const now = new Date();
            const formattedDate = `${now.getDate().toString().padStart(2, '0')}/${(now.getMonth() + 1).toString().padStart(2, '0')}/${now.getFullYear()}`;
            console.log("Auto date is...", formattedDate);
            this.tasks.date = formattedDate;

        }
    },
    mounted(){
        this.getCurrentDate();
    }

}
</script>