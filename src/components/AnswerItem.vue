<template>
  <li>
    <label v-if="typeQ === 1"
      ><input
        name="answer"
        type="radio"
        :value="answer.id"
        @change="$emit('picked', answer)"
        v-model="selected"
      />{{ answer.text }}</label
    >
    <label v-else
      ><input
        name="answer"
        type="checkbox"
        :value="answer.id"
        @change="$emit('picked', answer)"
        v-model="selected"
      />{{ answer.text }}</label
    >
  </li>
</template>

<script>
export default {
  props: {
    answer: {
      type: Object,
      requared: true,
    },
    selected: {
      type: Number,
    },
    typeQ: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      checked: false,
    };
  },
  methods: {
    checkState() {
      console.log(selected.id);
      if (selected.id === anwser.id) return true;
      else return false;
    },
  },
  watch: {
    // selected() {
    //      console.log(selected)
    // }
  },
};
</script>

<style scoped>
li {
  font-size: 20px;
  height: 30px;
}
</style>
