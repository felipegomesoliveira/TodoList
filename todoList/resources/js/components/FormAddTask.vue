<template>
  <div>
    <div class="input-group mb-3">
    <input v-model="task" type="text" class="form-control" placeholder="you task here" aria-label="Server">
    <button @click="addTask()" type="button" class="btn btn-outline-secondary">
      <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-plus-square" viewBox="0 0 16 16">
        <path d="M14 1a1 1 0 0 1 1 1v12a1 1 0 0 1-1 1H2a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1h12zM2 0a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V2a2 2 0 0 0-2-2H2z"/>
        <path d="M8 4a.5.5 0 0 1 .5.5v3h3a.5.5 0 0 1 0 1h-3v3a.5.5 0 0 1-1 0v-3h-3a.5.5 0 0 1 0-1h3v-3A.5.5 0 0 1 8 4z"/>
      </svg>
      <span class="visually-hidden">Add Task</span>
    </button>
</div>
  </div>
</template>

<script>
export default {
    data: function () {
      return {
        task: '',
        user_id: Number('5')
      }
    },
    methods: {
      addTask(){
        const payload = {
          'user_id': {'user_id': this.user_id},
          'task': {'task': this.task}
        }
        if(this.task.task == ''){
          return
        }
         fetch(`http://127.0.0.1:8000/api/task/store`, {
                method: 'POST',
                headers: {
                    'Content-Type':'application/json',
                },
                body: JSON.stringify(payload)
            }).then(response => response.json() )
              .then( res => {
                 if(res.status == 201){
                   this.task.task == "";
                   console.log('deu certo');
                 }
              })
              .catch( error => {
                console.log(error);
              })
              
      }
    }
};
</script>

<style scoped>

</style>