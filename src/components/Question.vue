<template>
    <div>
        <h3><strong>{{ qNumber + 1 }}. </strong>{{ question }}</h3>
    </div>
</template>

<script>
    export default {
        props: {
            question: {
                type: String,
                required: true,
            },
            qNumber: Number,
        },
    }
</script>

<style scoped>


</style>