<template>
  <div class="container">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <!-- <router-view/> -->
    <h1>Психологический тест</h1>
    <hr />
    <div v-if="!isCompleted">
      <question :question="getQuestion" :qNumber="curInxQst" />
      <answer-list
        :answerOptions="getAnswerOptions"
        :qType="getQuestionType"
        :checkedAnswers="curAnswer"
        :qCurrent="curInxQst"
        @picked="handleChange"
      />
      <div class="btns">
        <my-button @click="prevQ" :disabled="forbiddenPrev"> Назад</my-button>
        <my-button @click="nextQ" :disabled="forbiddenNext">
          {{ buttonText }}</my-button
        >
      </div>
    </div>
    <div v-if="isCompleted">
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
      forbiddenNext: true,
      buttonText: "Далее",
      isCompleted: false,
      initially: false,
      questionsList: [
        {
          id: 1,
          qtype: "radio",
          questionText: "Работа в команде или в одиночестве?",
          answerOptions: ["В команде", "В одиночестве", "Никак"],
        },
        {
          id: 2,
          qtype: "checkbox",
          questionText: "Теория или практика?",
          answerOptions: ["Теория", "Практика", "Все вместе"],
        },
        {
          id: 3,
          qtype: "checkbox",
          questionText:
            "Телефонный звонок или электронные письма (текстовые сообщения)?",
          answerOptions: [
            "Телефонный звонок",
            "Электронные письма (текстовые сообщения)",
          ],
        },
        {
          id: 4,
          qtype: "radio",
          questionText: "Утро или ночь?",
          answerOptions: ["Утро", "Ночь"],
        },
        {
          id: 5,
          qtype: "radio",
          questionText: "Пляж или горы?",
          answerOptions: ["Пляж", "Горы"],
        },
        {
          id: 6,
          qtype: "radio",
          questionText: "Вечеринка в клубе или дома?",
          answerOptions: ["Вечеринка в клубе", "Дома"],
        },
        {
          id: 7,
          qtype: "radio",
          questionText: "Спонтанность или планирование?",
          answerOptions: ["Спонтанность", "Планирование"],
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
      userAnswers: [],
      userAnswer: [],
    };
  },
  methods: {
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
    handleChange(obj) {
      let index = obj[0];
      let checked = obj[1];

      if (this.questionsList[this.curInxQst].qtype !== "radio") {
        if (checked) {
          if (!this.userAnswer.includes(index)) this.userAnswer.push(index);
        } else {
          this.userAnswer = this.userAnswer.filter((x) => x !== index);
        }
      } else this.userAnswer = [index];
      this.userAnswers[this.curInxQst] = this.userAnswer.slice();

      // if (this.userAnswer.length === 0) {
      //   this.forbiddenNext = true;
      // } else this.forbiddenNext = false;
      this.canOpenNextPage();
    },
    canOpenNextPage() {
      console.log("can or not?");
      if (this.userAnswer.length === 0) {
        this.forbiddenNext = true;
      } else this.forbiddenNext = false;
    },
  },
  computed: {
    getQuestion() {
      return this.questionsList[this.curInxQst].questionText;
    },
    getAnswerOptions() {
      return this.questionsList[this.curInxQst].answerOptions;
    },
    // getSelectedAnswer() {
    //   return this.questionsList[this.curInxQst].answer;
    // },
    getQuestionType() {
      console.log(this.questionsList[this.curInxQst].qtype);
      return this.questionsList[this.curInxQst].qtype;
    },
    curAnswer() {
      if (this.userAnswers[this.curInxQst]) {
        return this.userAnswers[this.curInxQst];
      } else {
        return [];
      }
    },
  },
  watch: {
    curInxQst(newValue, oldValue) {
      // console.log(newValue);
      if (newValue === 0) {
        this.forbiddenPrev = true;
      } else this.forbiddenPrev = false;

      // if (this.userAnswer.length === 0) {
      //   this.forbiddenNext = true;
      // } else this.forbiddenNext = false;

      if (this.userAnswers[newValue] !== undefined) {
        this.userAnswer = this.userAnswers[newValue];
      } else {
        this.userAnswer = [];
      }
      this.canOpenNextPage();
    },
    // userAnswer() {
    //   if (this.userAnswer.length === 0) {
    //     this.forbiddenNext = true;
    //   } else this.forbiddenNext = false;
    // },
    initially() {
      if (this.initially) {
        this.buttonText = "Далее";
        this.curInxQst = 0;
        this.isCompleted = false;
        this.initially = false;
        this.userAnswers = [];
        this.userAnswer = [];
        // for (let i = 0; i < this.questionsList.length; i++) {
        //   this.questionsList[i].answer = {};
        // }

        console.log("clear");
      }
    },
  },
  // created () {
  //   this.list.forEach((val) => {
  //     this.$watch(() => val, this.canNextPage, {deep: true});
  //   });
  // },
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
