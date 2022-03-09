<template>
    <div class="todoListContainer">
        <div class="heading">
            <h1 id="title">To Do List </h1>
            <add-task-form
            v-on:reloadlist="getList()"/>
        </div>
        <list-view
        :tasks="tasks"
        v-on:reloadlist="getList()"/>
    </div>
</template>

<script>
import addTaskForm from "./addTaskForm.vue"
import listView from "./listView.vue"
export default{
    components: {
        addTaskForm,
        listView
    },
    data: function(){
        return{
            tasks: []
        }
    },
    methods:{
        getList(){
            axios.get('api/tasks')
            .then(response =>{
                this.tasks = response.data
            })
            .catch(error=>{
                console.log( error);
            })
        }
    },
    created(){
        this.getList();
    }

}

</script>
<style scoped>
.todoListContainer{
    width: 350px;
    margin: auto;
}
.heading{
    background: #E6E6E6;
    padding: 10px;
}
.title{
    text-align: center;
}
</style>