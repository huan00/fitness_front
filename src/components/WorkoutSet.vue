<template>
  <div class="set-page">
    <div class="set-input ">
      <label>Set Number: </label>
      <input type="number" placeholder="Set" :value="set" disabled >
    </div>
    <div class="set-input ">
      <label>Rep Number: </label>
      <input type="number" name="rep" placeholder="Rep" v-model='rep' @blur="setWorkoutData" />
    </div>
    <div class="set-input ">
      <label>Weight(lb): </label>
      <input type="number" name="weigth" placeholder="Weight/lb" v-model='weight' @blur="setExerciseSet"
      />
    </div>
    </div>
</template>

<script>
export default {
  name: 'WorkoutSet.vue',
  props:{
    set: Number,
    exercise_set: Array
  },
  data(){
    return {
      rep: '',
      weight: '',
    }
  },
  methods: {
    setWorkoutData(event){
      const value = {set: this.set, rep: this.rep, weight: this.weight}
      if(this.rep !== '' && this.weight !== ''){
        // console.log(value)
        this.$emit('customChange', value)
      }
    },
    setExerciseSet(event){
      if(this.rep && this.weight){
        const temp = {rep: this.rep, weigth: this.weight, set: this.set}
        this.exercise_set.push(temp)

      }
      console.log(this.exercise_set)
    }
  }
}
</script>

<style>
.set-page {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;

  padding: 10px 0;
}
.set-input {
  display: flex;
  text-align: left;
  align-items: center;
}
.set-input label {
  flex: 1
}
.set-input input {
  flex: 2;
  margin: 5px 0;
  padding: 5px 5px;
}
</style>