<template>
  <div class="home">
    <div class="home-date">
      <h1>{{new Date().toDateString().slice(0, 10)}}</h1>
    </div>
    <div class="exercise-img">
      <img :src="exerciseList[0]?.gifUrl" />
    </div>
    
    <WorkoutHistory
    v-for = "exercise in exerciseList.slice(0, 10)" 
    v-bind:key = "exercise.id" 
    v-bind:exercise = "exercise"
    />
    
      <div class="workoutBtn">
        <button class="workoutBtn-cal">Calculator</button>
        <router-link to="recordworkout"><button class="workoutBtn-record">Record</button></router-link>
      </div>

  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios'
import WorkoutHistory from '@/components/WorkoutHistory.vue'

export default {
  name: 'HomeView',
  components: {
    WorkoutHistory,

},
  data(){
    return {
      exerciseList: []
    }
  },
  mounted(){
    if(localStorage.getItem('exerciseList')){
      this.exerciseList = JSON.parse(localStorage.getItem('exerciseList'))
    }else{

      this.getExerciseList()
    }
  },
  methods:{
    async getExerciseList(){
      const res = await axios.get('https://exercisedb.p.rapidapi.com/exercises',
        {
          headers: {
            'X-RapidAPI-Key': '93ca3a18dbmshe726aeae2cb1c33p1ec27ajsn9fc9e9dc0389',
            'X-RapidAPI-Host': 'exercisedb.p.rapidapi.com'
          }
        })
    
    localStorage.setItem('exerciseList', JSON.stringify(res.data))
    this.exerciseList = res.data
    }
  },
}
</script>

<style>
  .home {
    width: 480px;
    height: 844px;
    height: auto;
    margin: 0 auto;
    
  }
  .home-date{
    
    text-align: left;
  }



</style>