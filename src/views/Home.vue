<template>
  <div class="home">
    <div v-if="tasks.length">
      <div v-for="task in tasks" :key="task.id">
        <Task :task="task" @delete="handleDelete" @toggleComplete="handleToggleComplete"/>
      </div>
    </div>
  </div>
</template>

<script>
import Task from "@/components/Task.vue";

export default {
  name: "Home",
  components: { Task },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    handleDelete(id) {
      this.tasks = this.tasks.filter(task => {
        return task.id !== id
      })
    },
    handleToggleComplete(id){
      this.tasks.forEach(task => {
        if (task.id == id){
          task.complete =! task.complete;
        }
      });
    }
  },
  mounted() {
    fetch("http://localhost:3000/tasks")
        .then((res) => res.json())
        .then((data) => (this.tasks = data))
        .catch((err) =>
          console.log(
            "something went wrong while reading the json file: " + err.message
          )
        );
  },
 
};
</script>
<style>
</style>
