<template>
  <div id="container">
    <h1 id="title">Torre - User Skills </h1>
    <CustomInput v-model="username" />
    <button @click="fetchUser" id="buttonskills">Show Skills</button>
    <img id="profileimg" v-bind:src="user.picture" alt="">
    <h2 id="name">{{ user.name }}</h2>
    <div>
      <ul>
        <li v-for="(skill, index) in user.skills" :key="index" id="list">{{ skill.name }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import CustomInput from './components/CustomInput.vue';

export default {
  components: { CustomInput },
  data() {
    return {
      user: {
        name: '',
        picture: '',
        skills: [],
        proficiency: ''
      },
      username: 'getuser'
    }
  },

  //Get user Axios
  methods: {
    fetchUser() {
      axios
        .get(`https://torre-api-henna.vercel.app/users/${this.username}`)
        .then((response) => {
          this.user.name = response.data.person.name
          this.user.skills = response.data.strengths
          this.user.picture = response.data.person.picture
        })
        .catch((error) => {
          console.log(error)
        })
    }
  }
}
</script>

<style scoped></style>
