<template>
    <div>
        <div v-for="(tasks, index) in tasks" :key="index">
            <list-task
            :tasks = "tasks"
            class="tasks"
            v-on:taskchanged="$emit('reloadlist')"/>
        </div>
    </div>
</template>

<script>
import listTask from "./listTask.vue"
export default{
    props: ['tasks'],
    components:{
        listTask
    }
}

</script>
<style scoped>
.tasks{
    background: #e6e6e6;
    padding: 5px;
    margin-top:5px;
    
}
</style>