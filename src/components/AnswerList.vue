<template>
  <div>
    <ul class="answer__options">
      <answer-item
        v-for="(item, index) in answerOptions"
        :selected="tmp(index)"
        :text="item"
        :key="index"
        :value="index"
        :qType="qType"
        :idx="index"
        :qCurrent="qCurrent"
        
        @picked="handleChange"
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
    qType: {
      type: String,
      required: true,
    },
    qCurrent: Number,
    checkedAnswers: {
      //выбранные ответы на вопрос
      type: Array,
      required: true
    },
  },

  components: { AnswerItem },
  methods: {
      tmp(index) {
              for(let i=0; i< this.checkedAnswers.length; i++)
                console.log('checked', this.checkedAnswers[i])

          if (this.checkedAnswers.length) {

            return this.checkedAnswers.includes(index.toString())
          } else return false
      },

    handleChange(obj) {
      console.log("answerList: ", obj);
      this.$emit('picked', obj)
    },
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
