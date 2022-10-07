<template>
  <div class="set-page">
  
    <div class="set-input ">
      <label>Set Number: </label>
      <input type="number" placeholder="Set" :value="set" disabled>
    </div>
    <div class="set-input ">
      <label>Rep Number: </label>
      <input type="number" placeholder="Rep" />
    </div>
    <div class="set-input ">
      <label>Weight(lb): </label>
      <input type="number" placeholder="Weight/lb" />
    </div>
    </div>
</template>

<script>
export default {
  name: 'WorkoutSet.vue',
  props:{
    set: Number
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