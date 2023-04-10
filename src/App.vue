<template>
  <div id="container">
    <h1 id="title">Torre - User Skills </h1><br>
    <CustomInput v-model="username"/><br>
    <button @click="fetchUser">Show Skills</button><br>
    <h2 id="name">{{ user.name }}</h2><br>
    <img v-bind:src="user.picture" alt=""><br>
    <ul>
      <li v-for="(skill, index) in user.skills" :key="index">{{ skill.name }}</li>
    </ul>
  </div>
  
</template>

<script>
import axios from "axios";
import CustomInput from './components/CustomInput.vue';

export default {
  components: { CustomInput },
   data(){
    return {
      user: {
        name: '',
        picture: '',
        skills: []
      },
      username : 'getuser' 
    }
   },

//Get user Axios
   methods: {
    fetchUser () {
      console.log(this.username)
      axios
        .get(`https://torre-api-henna.vercel.app/users/${this.username}`) 
        .then((response) => {
          console.log(response.data)
          this.user.name = response.data.person.name
          this.user.skills = response.data.strengths
          this.user.picture = response.data.person.picture
          console.log(this.user.name)
        })
        .catch((error) => {
          console.log(error)
        })
    }
  }
}
</script>

<style scoped>
 #title{
  color: aliceblue;
  text-align: center;
 }

 #container{
  padding: 40px 80px;
  border: rgb(139, 141, 141) 2px solid;
  border-radius: 10px;
  background-color: #27292d;
  margin-top: 10%;
 }

 #name{
  color: aliceblue;
  text-align: center;
  margin-top: 10%;
 }
</style>
