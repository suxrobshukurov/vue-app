<template>
  <div class="user">
    <button type="button" @click="getUser">Получить пользователя</button>
    <button type="button" @click="getRandomBeer">Получить пиво</button>
    <p>{{ user.first_name }}</p>
    <p>{{ user.avatar }}</p>
    <p>{{ dateOfBirth }}</p>
    <p>{{ userEmployment }}</p>
    <p>{{ userAge }}</p>


  </div>
</template>

<script>
import axios from 'axios';
import moment from 'moment';
export default {
  name: "App",
  data() {
    return {
      user: [],
      dateOfBirth: '',
      userAge: '',
      beer: {},
      userEmployment: '',
    }
  },
  methods: {
    getUserAge(date_of_birth) {
      return moment().diff(date_of_birth, 'years', false);
    },
    async getUser() {
      try {
        const response = await axios.get('https://random-data-api.com/api/users/random_user');
        this.user = response.data;
        this.dateOfBirth = this.user.date_of_birth;
        this.userEmployment = this.user.employment.title
        console.log(response.data);
      } catch (error) {
        console.log(error)
      }
    },
    async getRandomBeer() {
      try {
        const response = await axios.get('https://random-data-api.com/api/beer/random_beer');
        this.beer = response.data;
        console.log(response.data);
      } catch (error) {
        console.log(error)
      }
    }
  },
  mounted() {
    this.getUser();
    this.getUserAge(this.user.date_of_birth);
  }
}
</script>

<style scoped>

</style>