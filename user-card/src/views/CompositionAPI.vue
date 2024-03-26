<script setup>
import axios from "axios";
import {onMounted, ref} from "vue";

const loading = ref(true)
const error = ref(false)
const user = ref(null)
const isOverView = ref(true)

onMounted(async () => {
  await axios.get('https://randomuser.me/api/')
    .then((res) => {
      setTimeout(() => {
        const {
          gender,
          email,
          name: { title, first, last },
          location: { city, country },
          login: { username, password },
          dob: { age },
          phone,
          picture: { large },
        } = res.data.results[0];
        user.value = {
          gender,
          email,
          name: { title, first, last },
          location: { city, country },
          login: { username, password },
          dob: { age },
          phone,
          picture: { large },
        }
        loading.value = false
      }, 5000)
    }).catch((err) => {
      console.log(err)
      error.value = true
    })
})

const listName = () => {
  return ` ${user.value.name.title}. ${user.value.name.first} ${user.value.name.last}`
}

const handleOverView = () => {
isOverView.value = !isOverView.value
}

const reloadCard = () => {
  window.location.reload();
}

</script>

<template>
  <div class="app">
    <div class="loading" v-if="loading">
      <svg
        height="50"
        viewBox="0 0 100 100"
        width="50"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
      >
        <circle
          cx="50"
          cy="50"
          fill="none"
          r="30"
          stroke="#211951"
          stroke-width="10"
        />
        <circle
          cx="50"
          cy="50"
          fill="none"
          r="30"
          stroke="#FFF"
          stroke-dasharray="90"
          stroke-dashoffset="45"
          stroke-width="10"
        >
          <animateTransform
            attributeName="transform"
            attributeType="XML"
            dur="1.5s"
            from="0 50 50"
            repeatCount="indefinite"
            to="360 50 50"
            type="rotate"
          />
        </circle>
      </svg>
    </div>
    <div v-else-if="error">
      <h1>Error loading user</h1>
    </div>
    <div v-else class="card">
      <div class="profile_photo">
        <img :src="user.picture.large" :alt="user.name.first">
      </div>
      <div class="buttons">
        <p @click="handleOverView">Over view</p>
        <p @click="handleOverView">About</p>
      </div>
      <div class="user-info">
        <div v-if="isOverView" class="overview">
          <p>Name: {{ listName() }} </p>
          <p>Gender: {{ user.gender }}</p>
          <p>Age: {{ user.dob.age }}</p>
          <p>Username: {{ user.login.username }}</p>
        </div>
        <div v-else class="about">
          <p>Email: {{ user.email }}</p>
          <p>City: {{ user.location.country }} / {{ user.location.city }}</p>
          <p>Phone: {{ user.phone }}</p>
          <p>Password: {{ user.login.password }}</p>
        </div>
      </div>
      <button @click="reloadCard">Reload Card</button>
    </div>
  </div>
</template>

<style scoped>

img {
  border: #c3c3c3 3px solid;
  border-radius: 100%;
  margin: 2rem;
}

button {
  background: #211951;
  color: #FFF;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
}

.app {
  margin: auto;
}

.card {
  background: #1F1E1F;
  color: #D8D9D9;
  width: 45%;
  height: 50%;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  align-items: center;
  justify-content: center;
}

.buttons {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: center;
  gap: 20px;
  border-bottom: 3px solid #c3c3c3;
}

.buttons > p {
  border: none;
  text-align: center;
  background: #1F1E1F;
  color: #D8D9D9;
}
.loading {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

@media (min-width: 768px) {
  .card {
    width: 20%;
    height: 10%;
  }
}

</style>
