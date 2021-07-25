<template>
  <button>
    <slot></slot>
  </button>
</template>

<script>
export default {};
</script>

<style scoped>
button {
  border: 1px solid #0066cc;
  background-color: #0099cc;
  color: #ffffff;
  padding: 5px 10px;
  font-size: 20px;
  width: 130px;
}

button:hover {
  border: 1px solid #0099cc;
  background-color: #00aacc;
  color: #ffffff;
  padding: 5px 10px;
}

button:disabled {
  border: 1px solid #999999;
  background-color: #cccccc;
  color: #666666;
}
</style>
