<template>
  <div class="home">
    <v-text-field
    class="pa-3"
    v-model="newTaskTitle"
            outlined
            label="Add Task"
            append-icon="mdi-plus"
            hide-details
            clearable
            @click:append="addTask"
            @keyup.enter="addTask"
          ></v-text-field>
          <div v-if="tasks.length">

            <v-list flat class="pt-0">
              
              <div v-for="task in tasks" :key="task.id">
        <v-list-item @click="doneTask(task.id)" :class="{ 'blue lighten-5': task.done }">
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title :class="{ 'text-decoration-line-through': task.done }">{{ task.title }}
              </v-list-item-title>
            </v-list-item-content>
            <v-list-item-action>
            <v-btn 
            icon
            @click.stop="deleteTask(task.id)"
            >
              <v-icon color="error">mdi-delete</v-icon>
            </v-btn>
          </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
    <div v-else>
      <v-icon color="blue" large>
        mdi-check
      </v-icon>
      <h3>All Tasks completed</h3>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      newTaskTitle:'',
      tasks: [
        // {
        //   id: 1,
        //   title: "Wake up",
        //   done: false,
        // },
        // {
        //   id: 2,
        //   title: "Buy phone",
        //   done: false,
        // },
        // {
        //   id: 3,
        //   title: "Go to work",
        //   done: false,
        // },
      ],
    };
  },
  methods: {
    addTask(){
      let newTask = {
        id: Date.now(),
        title: this.newTaskTitle,
        done:false,
      }
      this.tasks.push(newTask);
      this.newTaskTitle=''
    },
    doneTask(id) {
      let task = this.tasks.filter(task => task.id === id)[0]
      task.done = !task.done
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter(task => task.id!== id)
    }
  }
};
</script>
