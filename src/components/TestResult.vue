<template>
  <div class="result">
    <h3>Ваш результат</h3>
    <div class="result__text">{{result.text}}</div>
  </div>
  <my-button class="result__btn" @click="$emit('init')">В начало </my-button>
</template>

<script>
import MyButton from '@/components/UI/MyButton.vue';
export default {
  components: { MyButton },
    props: {
        result: {
            type: Object,
            required: true, 
        },
    },
};
</script>

<style scoped>
.result {
  /* height: 160px; */
}
.result__text {
    font-size: 18px;
    font-style: italic;
}
.result__btn {
    margin: 20px 0 0 0;
}
</style>
