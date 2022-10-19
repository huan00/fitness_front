<template>
  <div class="workoutHistory-page">
      <div class="maxRep">
        <p class="rep">1 rep max</p>
      </div>
      <div class="workoutName">
        <h1>{{exercise.name}}</h1>
        <h1>130lb</h1>
      </div>
  </div>
</template>

<script>
export default {
  name: 'WorkoutHistory',
  props: {
    exercise: Object,
  },
}
</script>

<style>
  .workoutHistory-page{
    display: flex;
    flex-direction: column;
  }
  .maxRep {
    text-align: left;
  }
  .workoutName {
    display: flex;
    justify-content: space-between;
  }
  .workoutBtn {
    display: flex;
    justify-content: space-around;
  }
  .workoutBtn-sec {
    height: 50px;
    width: 150px;
    
    border-radius: 30px;
    border: 1px solid #CCC;
    padding: 0 20px;
  }

.workoutBtn-primary {
    height: 50px;
    width: 200px;

    border-radius: 30px;
    border: 1px solid black;
    background-color: black;
    color: white;
    font-size: 24px;
    cursor: pointer;
  }

  .workoutBtn-primary:hover {
    background-color: green;
    border: none;
  }
</style>