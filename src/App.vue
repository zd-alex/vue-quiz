<template>
  <div class="container">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <!-- <router-view/> -->
    <h1>Психологический тест</h1>
    <hr />
    <question :question="getQuestion" />
    <answer-list v-bind:answerOptions="getAnswerOptions" @picked="gotMessage" />
    <div class="btns">
      <my-button @click="prevQ" :disabled="forbiddenPrev"> Назад</my-button>
      <my-button @click="nextQ" :disabled="forbiddenNext"> Далее</my-button>
    </div>
  </div>
</template>

<script>
import Question from "@/components/Question";
import AnswerList from "@/components/AnswerList";
import MyButton from "@/components/UI/MyButton";

export default {
  components: {
    Question,
    AnswerList,
    MyButton,
  },
  data() {
    return {
      curInxQst: 0,
      forbiddenPrev: true,
      forbiddenNext: false,
      questionsList: [
        {
          id: 1,
          qtype: 1,
          questionText: "Работа в команде или в одиночестве?",
          completed: false,
          answerOptions: [
            { id: 1, text: "В команде" },
            { id: 2, text: "В одиночестве" },
          ],
        },
        {
          id: 2,
          qtype: 1,
          questionText: "Теория или практика?",
          completed: false,
          answerOptions: [
            { id: 1, text: "Теория" },
            { id: 2, text: "Практика" },
          ],
        },
        // {
        //   id: 3,
        //   qtype: 1,
        //   questionText:
        //     "Телефонный звонок или электронные письма (текстовые сообщения)?",
        //   completed: false,
        //   answerOptions: [
        //     { id: 1, text: "Телефонный звонок" },
        //     { id: 1, text: "Электронные письма (текстовые сообщения)" },
        //   ],
        // },
        {
          id: 4,
          qtype: 1,
          questionText: "Утро или ночь?",
          completed: false,
          answerOptions: [{id: 1, text: "Утро"}, {id: 1, text: "Ночь"}],
        },
        {
          id: 5,
          qtype: 1,
          questionText: "Пляж или горы?",
          completed: false,
          answerOptions: [{id: 1, text: "Пляж"}, {id: 1, text: "Горы"}],
        },
        {
          id: 6,
          qtype: 1,
          questionText: "Вечеринка в клубе или дома?",
          completed: false,
          answerOptions: [{id: 1, text: "Вечеринка в клубе"}, {id: 2, text: "Дома"}],
        },
      ],

      // userAnswers: [],
      // curAnswer: {},
    };
  },
  methods: {
    gotMessage(obj) {
      // console.log('i have got a message ', obj)
      // this.curAnswer = obj
      this.questionsList[this.curInxQst].answer = obj;
    },
    nextQ() {
      // let curQuestion = this.questionsList[(this.curInxQst)]
      // curQuestion.answer = this.curAnswer
      // this.userAnswers.push(curQuestion.answer)

      if (this.curInxQst < this.questionsList.length - 1) {
        this.curInxQst += 1;
      }
    },
    prevQ() {
      if (this.curInxQst > 0) {
        this.curInxQst -= 1;
      }
    },
  },
  computed: {
    getQuestion() {
      return this.questionsList[this.curInxQst].questionText;
    },
    getAnswerOptions() {
      return this.questionsList[this.curInxQst].answerOptions;
    },
  },
  watch: {
    curInxQst(newValue) {
      // console.log(newValue);
      if (newValue === 0) {
        this.forbiddenPrev = true;
      } else this.forbiddenPrev = false;

      if (newValue === this.questionsList.length - 1) {
        this.forbiddenNext = true;
      } else this.forbiddenNext = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  background-color: #42b983;
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
.container {
  max-width: 700px;
  margin: 0 auto;
}
.btns {
  display: flex;
  margin: 25px;
  justify-content: space-around;
}
</style>
