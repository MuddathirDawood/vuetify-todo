<template>
  <div class="home">
    <v-text-field filled label="Add Task" append-icon="mdi-plus" hide-details clearable v-model="taskTitle"
     @click:append="addTask" @keyup.enter="addTask"></v-text-field>  
  <v-list flat class="pt-0">
    <div v-for="task in tasks" :key="task">
        <v-list-item @click="doneTask(task.id)" :class="{ 'green lighten-3' : task.done}">
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox
                :input-value="task.done"
                color="primary"
              ></v-checkbox>
            </v-list-item-action>
            
            <v-list-item-content>
              <v-list-item-title :class="{ 'text-decoration-line-through': task.done}">{{task.title}}</v-list-item-title>
            </v-list-item-content>

            <v-list-item-action>
              <v-btn icon @click.stop="deleteTask(task.id)">
                <v-icon color="grey darken-2">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
    
  </template>

<script>
  export default ({
  name: 'HomeView',
  data(){
    return{
      taskTitle: '',
      tasks:[
        {
          id: 1,
          title: 'Wake Up',
          done: false
        },
        {
          id: 2,
          title: 'Shower',
          done: false
        },
        {
          id: 3,
          title: 'Brush Teeth',
          done: false
        },
        {
          id: 4,
          title: 'Eat Lunch',
          done: false
        },
        {
          id: 5,
          title: 'Sleep',
          done: false
        },
      ]
    }
  },
  methods: {
    doneTask(id){
      let task = this.tasks.filter(task => task.id === id)
      console.log(task);
      task[0].done = !task[0].done
    },
    deleteTask(id){
      this.tasks = this.tasks.filter(task => task.id !== id)
    },
    addTask(){
      let newtask = {
        id: Date.now(),
        title: this.taskTitle,
        done: false
      }
      this.tasks.push(newtask);
      this.taskTitle = '';
    }
  },
});
</script>
