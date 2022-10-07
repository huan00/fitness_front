<template>
  <div class="recordWorkout-page">
    <div class="set-input ">
      <label>Enter workout set: </label>
      <input type="number" placeholder="Number of set" v-model="numberSet"/>
    </div>
    <div class="set-input workoutName-input">
      <label>Workout Name:</label>
      <input 
      type="text" 
      placeholder="Workout Name" 
      :value="workoutName"
      @input="event => workoutName = event.target.value"
      />
    </div>
    <div class="workoutName-filter-wrapper" v-if="filterName.length > 1">
      <p class="workoutName-filter" v-for="name in filterName" :key="name.id" @click="setWorkoutName(name.name)">{{name.name}}</p>
    </div>
    <div>
      <img src="http://d205bpvrqc9yn1.cloudfront.net/0001.gif" alt="exercise" />
    </div>
    <div class="workoutSet-wrapper">
      <WorkoutSet 
      v-for="n in numberSet"
      :key="n"
      v-bind:set="n"
      />
    </div>
    <div>
      <button>Cancel</button>
      <button>Save</button>
    </div>

  </div>
</template>

<script>

import WorkoutSet from '../components/WorkoutSet.vue';

export default {
    name: "RecordWorkout",
    components: { WorkoutSet },
    data(){
      return {
        numberSet: 0,
        exerciseData: [],
        workoutName: '',
        filterName: []
      }
    },
    mounted(){
      this.exerciseData = JSON.parse(localStorage.getItem('exerciseList'))
    },
    watch:{
      workoutName(newWorkout, oldWorkout){
        console.log(newWorkout)
        // console.log(this.exerciseData)
        this.filterWorkout(newWorkout)
        console.log(this.filterName)
      }
    },
    methods:{
      filterWorkout(workout){
        if(workout === ''){
          this.filterName = []
        }else{

          this.filterName = this.exerciseData.filter((exercise)=> {return exercise.name.includes(workout)})
        }
      },
      setWorkoutName(name){
        this.workoutName = name
        this.filterName = []
      }
    },
}
</script>

<style>
.recordWorkout-page{
  height: 844px;
  display: flex;
  flex-direction: column;
  overflow-y: hidden;
  position: relative;
}
.workoutName-input{
  position: relative;
}
.workoutSet-wrapper {
  display: flex;
  flex-direction: column;
  height: 300px;
  overflow: auto;

  border: 1px solid black;
}
.workoutName-filter-wrapper{
  display: flex;
  flex-wrap: wrap;
  height: 400px;
  overflow: scroll;

}
.workoutName-filter{
  background-color: #CCC;
  border-radius: 50px;
  width: fit-content;
  margin: 5px;
  padding: 5px 10px;
}
</style>