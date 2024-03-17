<script setup>
import { reactive, ref } from "vue";

const question = ref("")
const answer = ref("")
const cards = reactive([])

const handleCardCreate = () => {
  cards.push({
    question: question.value,
    answer: answer.value,
    showAnswer: false
  })
  question.value = ""
  answer.value = ""
}

const toggleAnswer = (card) => {
  card.showAnswer = !card.showAnswer
}
</script>

<template>
  <div class="container">
    <form @submit.prevent="handleCardCreate">
      <input type="text" placeholder="Question" v-model="question">
      <input type="text" placeholder="Answer" v-model="answer">
      <button>Create Card</button>
    </form>
    <ul>
      <li v-for="item in cards">
        <div @click="toggleAnswer(item)" class="card" :class="{ flipped: cards.showAnswer }">
          <div v-if="!item.showAnswer" class="card-front">
            <h3>{{ item.question }}</h3>
            <p>Cevabı Görmek Tıklayınız</p>
          </div>
          <p v-else class="card-back">{{ item.answer }}</p>
        </div>
      </li>
    </ul>
  </div>
</template>


<style>
  .container {
    width: 100vw;
    height: 100vh;
  }

  ul {
    list-style: none;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
  }

  .card {
    list-style: none;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 10px;
  }

  .card-front {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 300px;
    height: 300px;
    border-radius: 10px;
    background: #e0c6f6;
  }

  .card-back {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    align-items: center;
    width: 300px;
    height: 300px;
    border-radius: 10px;
    background: #f6c6ec;
  }

</style>
