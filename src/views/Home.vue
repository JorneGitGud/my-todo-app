<template>
  <div class="home">
    <div v-if="tasks.length">
      <div v-for="task in tasks" :key="task.id">
        <Task :task="task" />
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
.home{
  background-image: url'@/assets/images/canopy-by-jorne.jpg';
}
</style>
