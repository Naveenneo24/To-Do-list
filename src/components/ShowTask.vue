<template>
    <Navigation />
    <h1 class="text-center p-4 text-xl font-semibold">All task are showing here</h1>
    <div class="md:flex md:flex-wrap gap-8 justify-evenly">
        <table class="border-collapse w-full">
    <thead>
        <tr>
            <th class="text-center p-2 border">Task ID</th>
            <th class="text-center p-2 border">Task Status</th>
            <th class="text-center p-2 border">Created Date</th>
            <th class="text-center p-2 border">Task Description</th>
            <th class="text-center p-2 border">Actions</th>
            <th class="text-center p-2 border">Task Complete</th>
        </tr>
    </thead>
    <tbody>
        <tr v-for="item in Tasks" :key="item.id">
            <td class="text-center p-2 border">{{ item.id }}</td>
            <td class="text-center p-2 border">{{ item.status }}</td>
            <td class="text-center p-2 border">{{ item.date }}</td>
            <td class="text-center p-2 border">{{ item.newTask }}</td>
            <td class="text-center p-2 border">
                <RouterLink :to="'/update-task/' + item.id" class="bg-black block p-2 text-center rounded text-white">UPDATE TASK</RouterLink>
                <button type="button" class="bg-[#FF0000] w-full px-4 py-2 rounded text-white" v-on:click="Taskdelete(item.id)">DELETE TASK</button>
            </td>
            <td class="text-center p-2 border">
                <input type="checkbox" v-model="item.isChecked" @change="taskUpdate(item)"> Task Complete
            </td>
        </tr>
    </tbody>
</table>


    </div>
</template>

<script>
import Navigation from './Navigation.vue';
import axios from 'axios';

export default {
    name: 'ShowTask',
    components: {
        Navigation
    },
    data() {
        return {
            tasks: {
                isChecked: true
            },
            Tasks: []
        }
    },
    methods: {
        async Taskdelete(id) {
            let result = await axios.delete("http://localhost:3000/tasks/" + id);
            console.log("Deleting...", result);
            if (result.status == 200) {
                alert("Task has been deleted");
                this.loadTask();
            }
        },
        async loadTask() {
            let result = await axios.get("http://localhost:3000/tasks");
            console.log("Results are ... ", result);
            this.Tasks = result.data;
        },
        async taskUpdate(task) {
            let result = await axios.put("http://localhost:3000/tasks/" + task.id, {
                status: this.tasks.isChecked ? 'Completed' : 'pending'
            });
            console.log("Updating...", result);
            if (result.status == 200) {
                alert("Task status updated");
                this.loadTask();
            }
        }
    },
    mounted() {
        this.loadTask();
    },
}
</script>