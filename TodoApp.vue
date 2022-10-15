<template>
  <div class = "container">
   <h2 class ="text-center mt-5">My Vue Todo App</h2>
   <!--input-->
   <div class="d-flex">
    <input v-model="task" type="text" placeholder="Enter Task" class="form-control">
    <button @click ="submitTask" class="btn btn-warning rounded-0">SUBMIT</button>
   </div>
   <!--Task Table-->
   <table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(tasks, index) in tasks" :key="index">
      <td>{{tasks.name}}</td>
      <td style="width: 120px"><span @click="changeStatus(index)" class="pointer">
           {{tasks.status}}
          </span>
        </td>
      <td>
        <div class="text-center" @click="editTask(index)">
          <span class="fa fa-pen pointer"></span>
        </div>
      </td>
      <td>
        <div class="text-center" @click="deleteTask(index)">
          <span class="fa fa-trash pointer"></span>
        </div>
      </td>
    </tr>
    
  </tbody>
</table>
     </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return{
      

      task: 'hello world',
      editedTask: null,
      availableStatuses: ['todo','in-progess','finished'],

      tasks: [
        {
          name: 'Steal bananas from the store.',
          status: 'todo'
      },
      {
        name: 'Eat 1kg glutony',
        status: 'todo'
      }
    ]
    }
  },
  methods: {
    submitTask(){
      if(this.task.length === 0) return;
      if(this.editedTask === null){
      this.tasks.push({
        name: this.task,
        status: 'todo'
      });
      this.task="";
     }else{
        this.tasks[this.editedTask].name = this.task; 
        this.editedTask = null;
     }
     this.task = '';
    },

    deleteTask(index){
      this.tasks.splice(index, 1);
    },
    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    changeStatus(index){
      let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
      if(++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.availableStatuses[newIndex];
    },
  }
  
};
</script>
<style scoped>
.pointer{
  cursor: pointer;
}
</style>


