<template>
  <div class="task">
    <div class="actions" @click="toggleDetails">
      <h3>{{ task.title }}</h3>
    </div>
    <div v-if="showDetails" class="details">
      <p>{{ task.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["task"],
  data(){
      return{
          showDetails: false
      }
  },
  methods:{
      toggleDetails(){
          this.showDetails = !this.showDetails;
      }
  }
}
</script>

<style>
.task{
    margin: 2rem auto;
    background: white;
    padding: 1rem 2rem;
    border-radius: 0.5rem;
    box-shadow: 0.4rem 0.8rem 1.2rem rgba(0,0,0,0.05);
    border-left: 0.5rem solid #5c90dd;
}
.actions h3{
    cursor: pointer;
}

.task {
	background: linear-gradient(-45deg, #e9724e21, #e73c7e0e, #23a5d51c, #23d5ab36);
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