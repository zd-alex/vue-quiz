<template>
    <li>
        <label><input name="answer" type="radio"
        @change.checked="$emit('picked', $event.target.value)"
        >{{ a }}</label>
    </li>
</template>

<script>
    export default {
        props: {
            a: {
                type: Text,
                requared: true,
            },
        },
    }
</script>

<style scoped>
li {
    font-size: 20px;
    height: 30px;
}


</style>