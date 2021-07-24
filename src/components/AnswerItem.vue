<template>
    <li>
        <label><input name="answer" type="radio"
        @change="$emit('picked', answer)"
        :checked="checked"
        >{{ answer.text }}</label>
    </li>
</template>

<script>
    export default {
        props: {
            answer: {
                type: Object,
                requared: true,
            },
        },
        data() {
            return {
                checked: false,
            }
        },
    }
</script>

<style scoped>
li {
    font-size: 20px;
    height: 30px;
}


</style>