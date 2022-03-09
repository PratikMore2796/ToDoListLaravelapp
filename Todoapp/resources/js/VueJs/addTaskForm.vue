<template>
    <div class="addTask">
        <input type="text" v-model="tasks.name"/>
        <font-awesome-icon icon="plus-square" 
        @click="addTask()"
        :class="[tasks.name ? 'active' : 'inactive', 'plus']"/>
    </div>
</template>

<script>
export default{
    data: function(){
        return{
            tasks:{
                name: ""
            }
        }
    },
    methods:{
        addTask(){
            if(this.tasks.name == ''){
                return;
            }

            axios.post('api/tasks/store',{
                tasks: this.tasks
            })
            .then( response =>{
                if(response.status = 201){
                    this.tasks.name = "";
                    this.$emit('reloadlist');
                }
            })
            .catch(error=>{
                console.log(error);
            })
        }
    }
}

</script>
<style scoped>
.addTask{
    display: flex;
    justify-content: center;
    align-items: center;
}
input {
    background: #f7f7f7;
    border:0px;
    outline: none;
    padding: 5px;
    margin-right: 10px;
    width: 100%;
}
.plus{
    font-size: 20px;

}
.active{
    color: #00ce25;
}
.inactive{
    color: #999;
}
</style>