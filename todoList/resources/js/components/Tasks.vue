<template>
    <div class="content">
       <input 
       type="checkbox" 
       @change="updatechech()"
       v-model="item.completed"
       />
       <span :class="[item.completed ? 'completed' : '', 'itemText' ]"> {{item.task}}</span>
        <button @click="removeTask()" type="button" class="btn btn-outline-secondary">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-trash" viewBox="0 0 16 16">
                <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z"/>
                <path fill-rule="evenodd" d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z"/>
            </svg>
                <span class="visually-hidden">Button</span>
        </button>
    </div>
</template>

<script>
export default {
   props:['item'],

   methods:{
       updatecheck (){
           fetch(`http://127.0.0.1:8000/api/task/${this.item.id} `, {
                method: 'PUT',
            }).then(response => response.json() )
              .then( res => {
                 if(res.status == 200){
                   this.$emit('taskChanged')
                 }
              })
              .catch( error => {
                console.log(error);
              })
       }
   }
}
</script>

<style scoped>
.completed{
    text-decoration: line-through;
    color:#9999;

}
.itemText{
    width: 100%;
    margin-left:20px;
}
.item{
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>