<template>
  <div class="recordWorkout-page">
    <div class="set-input ">
      <label>Workout Day: </label>
      <input type="date" v-model='workoutDate'/>
    </div>
    <div class="set-input ">
      <label>Focus Area: </label>
      <input type="text" v-model='focus_area'/>
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
    <div class="set-input ">
      <label>Enter workout set: </label>
      <input type="number" placeholder="Number of set" v-model="numberSet"/>
    </div>
    
    <div class="workoutName-filter-wrapper" v-if="filterName.length > 1">
      <p class="workoutName-filter" v-for="name in filterName" :key="name.id" @click="setWorkoutName(name.name)">{{name.name}}</p>
    </div>
    <div>
      <img :src="filterName[0]?.gifUrl" />
    </div>
    <div class="workoutSet-wrapper">
      <WorkoutSet 
      v-for="n in numberSet"
      :key="n"
      v-bind:set="n"
      v-bind:exercise_set = 'exercise_set'
      />
      <!-- @customChange="inputWorkoutData" -->
    </div>
    <div class="recordWorkout-Btn">
        <router-link to="/">
          <button class="workoutBtn-sec">Cancel</button>
        </router-link>
        <button class="workoutBtn-primary" @click="submitWorkoutData">Save</button>
    </div>

  </div>
</template>

<script>

import WorkoutSet from '../components/WorkoutSet.vue';
import axios from 'axios';

export default {
    name: "RecordWorkout",
    components: { WorkoutSet },
    data(){
      return {
        numberSet: 0,
        exerciseData: [],
        workoutName: '',
        focus_area: [],
        workoutDate: '',
        filterName: [],
        exercise_set: [],
        
      }
    },
    mounted(){
      this.exerciseData = JSON.parse(localStorage.getItem('exerciseList'))
    },
    watch:{
      workoutName(newWorkout, oldWorkout){
        this.filterWorkout(newWorkout)
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
      },
      // inputWorkoutData(value){
  
      //   const temp = {name: this.filterName[0].name, ...value}
      //   const tempArr = this.workoutData.filter((workout)=> {
      //      return workout.set !== temp.set})
      //   tempArr.push(temp)
      //   tempArr.sort((a,b)=>{ return a.set-b.set})
      //   this.workoutData = [...tempArr]
        
      // },
      async submitWorkoutData(){
        let submitData = {}
        if(this.filterName[0] && this.workoutDate && this.exercise_set && this.focus_area){
          submitData = {
            workout_day: this.workoutDate,
            focus_area: [this.focus_area.split(' ')],
            workout: [
              {
                exercise: this.filterName[0],
                exercise_set: this.exercise_set
              }
            ]
          }
          const res = await axios.post('http://localhost:8000/api/fitness/saveSession/', submitData)
          console.log(res)
        }
        this.$router.push('/')
      }
        
      

    },
}
</script>

<style>
.recordWorkout-page{
  height: 766px;
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
  height: 275px;
  overflow: auto;

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
.recordWorkout-Btn{
  width: 100%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  position: absolute;
  bottom: 0;
}

</style>