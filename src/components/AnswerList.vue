<template>
  <div>
    <ul class="answer__options">
      <answer-item 
      v-for="answer in answers" 
      v-bind:a="answer" 
      v-bind:key="answer.id"
      @picked="test"

      />

    </ul>
  </div>
</template>

<script>
import AnswerItem from "./AnswerItem";
export default {
  props: {
    answers: {
      type: Array,
      required: true,
    },
  },
  components: { AnswerItem },
  methods: {
      test(e) {
          console.log(e)
      }
  },
};
</script>

<style scoped>
.answer__options {
    list-style: none;
    text-align: left;
    /* height: 100px; */
}
</style>
