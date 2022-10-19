<template>
  <div class="signup-page">
    <div class="signup-title">
      <h1 class="title">Log In</h1>
      <form @submit.prevent="submitForm" class="signup-form">
        <div class="signup-input">
          <label>Username:</label>
          <input class="workout-input" type="text" placeholder="Enter desire username" v-model='username'/>
        </div>
        <div class="signup-input">
          <label>Password:</label>
          <input class="workout-input" type="password" placeholder="Enter desire password" v-model='password' />
        </div>
        <!-- <div class="signup-input">
          <label>Confirm Password:</label>
          <input class="workout-input" type="text" placeholder="Confirm Password" v-model="password2" />
        </div> -->
        <div class="signup-control">
          <button class="workoutBtn-primary" @click="submitForm">Log In</button>
          <p>Don't have an account? <router-link to="/signup">Click</router-link> to create an account</p>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
export default {
  name: 'LogIn',
  data(){
    return {
      username: '',
      password: '',
    }
  },
  methods:{
    
    async submitForm(){
      axios.defaults.headers.common['Authorization'] = ''
      localStorage.removeItem('token')
      const formData = {
        username: this.username,
        password: this.password
    }
      if(this.username !== '' && this.password !== ''){
      await axios.post("http://localhost:8000/api/fitness/token/login/", formData).then(response=>{
        const token = response.data.auth_token
        this.$store.commit('setToken', token)
        axios.defaults.headers.common['Authorization'] = 'Token ' + token
        localStorage.setItem('token', token)
        console.log(token)
        console.log('successful')}).catch(error=> console.log(error))
      }
      
    }
  },
}
</script>

<style>
  .signup-form {
    display: flex;
    flex-direction: column;
  }
  .signup-input {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    width: 100%;
    font-size: 18px;
  }
  .signup-input label {
    flex: 1;
  }
  .signup-input input {
    flex: 2;
    padding: 10px 20px;
    margin: 10px 0;
    
  }
  .workout-input {
    border-radius: 50px;
    border: 1px solid #CCC;
    font-size: 18px;
  }
</style>