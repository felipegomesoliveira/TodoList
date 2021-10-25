<template>
    <div class="container">
        <div class="heading">
            <h2 class="title">Todo List</h2>
            <form-add-task/>
            <div class="text-end">
          <button type="button" class="btn btn-warning"><a href="http://127.0.0.1:8000/user"> Edit user</a> </button>
      </div>
        </div>
        <list-task v-on:reloadList="getlist()" :items="task" />
    </div>
</template>

<script>
import formAddTask from './FormAddTask.vue';
import listTask from './ListTask.vue';
export default {
    components:{
        formAddTask,
        listTask
    },

     data: function (){
         return{
             task:[]
         }
        
    },

    methods: {
        getlist (){
             fetch(`http://127.0.0.1:8000/api/tasks/5`, {
                method: 'get',
            }).then(response => response.json() )
              .then( res => {
                this.task = res.data.task
              })
              .catch( error => {
                console.log(error);
              })
        }
    },
    created(){
            this.getlist;
        }
}
</script>

<style scoped>
.content{
    width: 350px;
    margin: auto;
}
.heading{
    background: #E0FFFF;
    padding: 10px;
}
.title{
    text-align: center;
}
</style>