<template>
<div class="container">
<Header @toggle-add-task="toggleAddTask" title="Note" :showAddTask="showAddTask"/>
<div v-if="showAddTask">
  <AddTask @add-task="addTask" />
</div>

<Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"/>
</div>

</template>

<script>
import Header from './components/Header.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'
export default {
  name: 'App',
  components:{
    Header,
    Tasks,
    AddTask
  },
  data(){
    return{
      tasks:[],
      showAddTask: false
    }
  },
  methods:{
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    },
    addTask(task){
      this.tasks = [...this.tasks, task]
    },
    deleteTask(id) {
      if(confirm('vi soglasnie udalit')){
        this.tasks = this.tasks.filter((task)=> task.id !== id) 
      }
     
    },
   toggleReminder(id) {
     console.log(id);
    this.tasks = this.tasks.map((task)=> task.id === id ? {...task, reminder: !task.reminder} :
     task)
    }

  },

  created(){
    this.tasks = [
    {
      id:1,
      text:'Liverpool was created',
      day:'march 1st march 1999 at 2:30pm',
      reminder:true
    },
     {
      id:2,
      text:'Barcelona was created',
      day:'January 2st march 1999 at 1:30pm',
      reminder:true
    },
     {
      id:3,
      text:'Chalsea was created',
      day:'march 1st march 1989 at 2:30pm',
      reminder:false
    }
    ]
  }

}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;700&family=Poppins:wght@400;500;600;700&display=swap');

*{
box-sizing:border-box;
padding:0;
margin:0;
}
body{
  font-family: 'Poppins', sans-serif;
}
.container{
  max-width: 500px;
  margin:30px auto;
  overflow:auto;
  min-height:300px;
  border:1px solid steelblue;
  padding:30px;
  border-radius:5px;
}
.btn{
display:inline-block;
background: #000;
color:#fff;
border:none;
padding:10px 20px;
margin:5px;
border-radius:5px;
cursor:pointer;
text-decoration:none;
font-size: 15px;
font-family: inherit;
}
.btn:focus{
  outline:none;

}
.btn:active{
  transform:scale(0.98);
}
.btn-block{
  display:block;
  width: 100%;
}
</style>
