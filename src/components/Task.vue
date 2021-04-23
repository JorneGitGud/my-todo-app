<template>
  <div class="task">
    <div class="actions">
      <h3 @click="toggleDetails">{{ task.title }}</h3>
      <div class="icons">
        <span v-if="!showDetails" class="material-icons" @click="toggleDetails">
          keyboard_arrow_down
        </span>
        <span v-if="showDetails" class="material-icons" @click="toggleDetails">
          keyboard_arrow_up
        </span>
        <span class="material-icons">edit</span>
        <span @click="deleteTask" class="material-icons">delete</span>
        <span @click="toggleComplete" class="material-icons">done</span>
      </div>
    </div>
    <div v-if="showDetails" class="details">
      <p>{{ task.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["task"],
  data() {
    return {
      showDetails: false,
      uri: "http://localhost:3000/tasks/" + this.task.id,
    };
  },
  methods: {
    toggleDetails() {
      this.showDetails = !this.showDetails;
    },
    deleteTask() {
      fetch(this.uri, { method: "DELETE" })
        .then(() => this.$emit("delete", this.task.id))
        .catch((err) => console.log(err));
    },
    toggleComplete() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { "content-type": "application/json" },
        body: JSON.stringify({ complete: !this.task.complete }),
      })
      .then(() => this.$emit("toggleComplete", this.task.id))
      .catch((err) => console.log(err));
    },
  },
};
</script>

<style>
.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.material-icons {
  cursor: pointer;
  font-size: auto;
  margin: 0.2rem;
  color: rgb(155, 154, 154);
}

.material-icons:hover {
  color: rgb(66, 66, 66);
}
.icons {
}
.task {
  margin: 2rem auto;
  background: white;
  padding: 1rem 2rem;
  border-radius: 0.5rem;
  box-shadow: 0.4rem 0.8rem 1.2rem rgba(0, 0, 0, 0.05);
  border-left: 0.5rem solid #5c90dd;
}
.actions h3 {
  cursor: pointer;
}

.task {
  background: linear-gradient(-45deg, #fafafa, #e73c7e0e, #ffffff, #23d5ab36);
  background-size: 400% 400%;
  animation: gradient 15s ease infinite;
}

@keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
</style>