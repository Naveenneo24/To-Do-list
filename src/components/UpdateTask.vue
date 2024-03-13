<template>
    <Navigation />
    <div class="p-8">
        <div class="bg-[#3498db] w-3/4 md:w-1/2 m-auto p-6 rounded-lg shadow-md text-white">
    <h1 class="text-center text-2xl font-bold mb-4">Update Task</h1>
    <form action="">
        <table class="w-full">
            <tr>
                <td><label for="newTask" class="block text-sm font-semibold">Task Description:</label></td>
                <td><input type="text" v-model="tasks.newTask" id="newTask" placeholder="Write Here . . . ."
                        class="w-full px-4 py-2 rounded-md border border-white text-gray-800 focus:outline-none focus:border-[#2c3e50]"
                        required></td>
            </tr>
            <tr>
                <td><label for="status" class="block text-sm font-semibold">Task Status (Yes/No):</label></td>
                <td><input type="text" v-model="tasks.status" id="status"
                        placeholder="Have you completed this task? {Yes/No}"
                        class="w-full px-4 py-2 rounded-md border border-white text-gray-800 focus:outline-none focus:border-[#2c3e50]"
                        required></td>
            </tr>
            <tr>
                <td><label for="date" class="block text-sm font-semibold">Task Due Date:</label></td>
                <td><input type="date" v-model="tasks.date" id="date"
                        class="w-full px-4 py-2 rounded-md border border-white text-gray-800 focus:outline-none focus:border-[#2c3e50]"
                        required></td>
            </tr>
        </table>
        <button type="button" v-on:click="updateTask"
            class="w-full bg-[#2ecc71] px-4 py-2 rounded-md text-white hover:bg-[#27ae60] focus:outline-none focus:bg-[#27ae60] mt-4">
            Update Task
        </button>
    </form>
</div>

    </div>
</template>
<script>
import Navigation from './Navigation.vue';
import axios from 'axios';
export default {
    name: 'UpdateTask',
    components: {
        Navigation
    },
    data() {
        return {
            tasks: {
                newTask: '',
                date: '',
                status: ''
            }
        }
    },
    methods: {
        async updateTask() {
            let result = await axios.put('http://localhost:3000/tasks/' + this.$route.params.id, {
                newTask: this.tasks.newTask.trim(),
                date: this.tasks.date,
                status: this.tasks.status
            });
            console.log("putting data ares", result);

            if (result.status == 200) {
                this.$router.push({ name: 'ShowTask' });
            }
        }
    },
    async mounted() {
        let result = await axios.get("http://localhost:3000/tasks/" + this.$route.params.id);
        console.log("update ares dfddddd", result);
        this.tasks = result.data;

    }
}
</script>