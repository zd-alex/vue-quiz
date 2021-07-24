<template>
  <div>
    <ul class="answer__options">
      <answer-item 
      v-for="item in answerOptions" 
      v-bind:answer="item" 
      v-bind:key="item.id"
      @picked="$emit('picked', item)"
      />

    </ul>
  </div>
</template>

<script>

import AnswerItem from "./AnswerItem";
export default {
  props: {
    answerOptions: {
      type: Array,
      required: true,
    },
  },
  components: { AnswerItem },
  methods: {
    //   tmp(e) {
    //       console.log(e)
    //   }
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
