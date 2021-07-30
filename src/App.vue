<template>
  <div class="container">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <!-- <router-view/> -->
    <h1>Психологический тест</h1>
    <hr />
    <div v-show="!isCompleted">
      <question :question="getQuestion" />
      <answer-list
        v-bind:answerOptions="getAnswerOptions"
        v-bind:selected="getSelectedAnswer"
        v-bind:typeQ="getQuestionType"
        @picked="gotMessage"
      />
      <div class="btns">
        <my-button @click="prevQ" :disabled="forbiddenPrev"> Назад</my-button>
        <my-button @click="nextQ"> {{ buttonText }}</my-button>
      </div>
    </div>
    <div v-show="isCompleted">
      <test-result :result="randomResult()" @init="initially = true" />
    </div>
  </div>
</template>

<script>
import Question from "@/components/Question";
import AnswerList from "@/components/AnswerList";
import MyButton from "@/components/UI/MyButton";
import TestResult from "@/components/TestResult.vue";

export default {
  components: {
    Question,
    AnswerList,
    MyButton,
    TestResult,
  },
  data() {
    return {
      curInxQst: 0,
      forbiddenPrev: true,
      forbiddenNext: false,
      buttonText: "Далее",
      isCompleted: false,
      initially: false,
      questionsList: [
        {
          id: 1,
          qtype: 1,
          questionText: "Работа в команде или в одиночестве?",
          answer: {},
          completed: false,
          answerOptions: [
            { id: 1, text: "В команде" },
            { id: 2, text: "В одиночестве" },
          ],
        },
        {
          id: 2,
          qtype: 2,
          questionText: "Теория или практика?",
          answer: {},
          completed: false,
          answerOptions: [
            { id: 1, text: "Теория" },
            { id: 2, text: "Практика" },
            { id: 3, text: "Все вместе" },
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
          answer: {},
          completed: false,
          answerOptions: [
            { id: 1, text: "Утро" },
            { id: 1, text: "Ночь" },
          ],
        },
        {
          id: 5,
          qtype: 1,
          questionText: "Пляж или горы?",
          answer: {},
          completed: false,
          answerOptions: [
            { id: 1, text: "Пляж" },
            { id: 1, text: "Горы" },
          ],
        },
        {
          id: 6,
          qtype: 1,
          questionText: "Вечеринка в клубе или дома?",
          answer: {},
          completed: false,
          answerOptions: [
            { id: 1, text: "Вечеринка в клубе" },
            { id: 2, text: "Дома" },
          ],
        },
      ],
      quizResult: [
        {
          id: 1,
          text:
            "Вы экстраверт, который любит общество других людей и веселую жизнь. В повседневной жизни вы активны и очень энергичны. Что касается профессиональной жизни, то вы предприимчивы и ориентированы на результат. А так же вы без труда заводите новые знакомства и находите общие темы для разговора.",
        },
        {
          id: 2,
          text:
            "Вы интроверт предпочитаете спокойствие, тишину и одиночество. Вас можно назвать уравновешенной натурой, любите жить моментом и сосредотачиваться на чем-то одном. Что касается профессиональной сферы, то вы более дальновидны и у вас творческий подход к работе.",
        },
        {
          id: 3,
          text: "Вы бездельник! Займитесь делом!",
        },
        {
          id: 4,
          text: "Вы идиот! Что тут поделаешь :)",
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
      if (this.buttonText === "Завершить") {
        this.isCompleted = true;
        console.log("тест пройден");
      } else if (this.curInxQst < this.questionsList.length - 2) {
        this.curInxQst += 1;
      } else if (this.curInxQst === this.questionsList.length - 2) {
        this.curInxQst += 1;
        this.buttonText = "Завершить";
      }
    },
    prevQ() {
      if (this.curInxQst > 0) {
        this.curInxQst -= 1;
        this.buttonText = "Далее";
      }
    },
    randomResult() {
      let max = this.quizResult.length;
      let res = this.quizResult[Math.floor(Math.random() * max)];
      console.log(res);
      return res;
    },
  },
  computed: {
    getQuestion() {
      return this.questionsList[this.curInxQst].questionText;
    },
    getAnswerOptions() {
      return this.questionsList[this.curInxQst].answerOptions;
    },
    getSelectedAnswer() {
      return this.questionsList[this.curInxQst].answer;
    },
    getQuestionType() {
      console.log(this.questionsList[this.curInxQst].qtype)
      return this.questionsList[this.curInxQst].qtype;
    }
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
    initially() {
      if (this.initially) {
        this.buttonText = "Далее";
        this.curInxQst = 0;
        this.isCompleted = false;
        this.initially = false;
        for (let i = 0; i < this.questionsList.length; i++) {
          this.questionsList[i].answer = {};
        }
        
        console.log("clear");
      }
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
