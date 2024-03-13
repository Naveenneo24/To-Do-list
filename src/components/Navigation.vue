<template>
    <div class="bg-[#00FFFF] p-2 m-auto text-lg  flex justify-evenly">
        <div class="hover:bg-[#0000FF] hover:text-white p-2 rounded">
            <RouterLink to="/add-task">Add task</RouterLink>
        </div>
        <div class="hover:bg-[#0000FF] hover:text-white p-2 rounded">
            <RouterLink to="/show-task">Show all task</RouterLink>
        </div>
    </div>
</template>
<script>
    export default{
        name:'Navigation'
    }
</script>