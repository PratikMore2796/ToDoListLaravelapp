<template>
    <div class="tasks">
        <input
            type="checkbox"
            @change="updateCheck()"
            v-model="tasks.completed"
            />
            <span :class="[tasks.completed ? 'completed': '','taskText']">{{tasks.name}}</span>
            <button @click="removeTask()" class="trashcan">
                <font-awesome-icon icon = "trash"/>
            </button>
    </div>
</template>

<script>

export default{

    props: ['tasks'],
    methods: {
        updateCheck(){
            axios.put('api/tasks/'+ this.tasks.id,{
                tasks: this.tasks
            })
            .then( response =>{
                if(response.status = 200){
                    this.$emit('taskchanged');
                }

            })
            .catch( error=>{
                console.log(error);
            })
        },
        removeTask(){
            axios.delete('api/tasks/' + this.tasks.id)
            .then(response=>{
                if( response.status = 200){
                    this.$emit('taskchanged');
                }
            })
            .catch( error =>{
                console.log(error);
            })
        }
    }

}

</script>
<style scoped>
.completed{
    text-decoration: line-through;
    color: #999;
}
.taskText{
    width: 100%;
    margin-left: 20px;
}
.tasks{
    display: flex;
    justify-content: center;
    align-items: center;
}

.trashcan{

    background: #e6e6e6;
    border:none;
    color: #f00;
    outline: none;


}

</style>