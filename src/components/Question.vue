<template>
    <div>
        <h3>{{ question }}</h3>
    </div>
</template>

<script>
    export default {
        props: {
            question: {
                type: Text,
                required: true,
            },
        },
    }
</script>

<style scoped>


</style>