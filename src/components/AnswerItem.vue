<template>
  <li>
    <label>
      <input name='group'
        :type="qType"
        :value="idx"
        v-model="checked"
        :checked="checked"
              
        @change='updateInput'
      />{{ text }}
    </label>
  </li>
</template>

<script>

export default {
  props: {
    // modelValue: [String, Number],
    text: {
      type: String,
      requared: true,
    },
    qType: {
      type: String,
      required: true,
    },
    selected: {
      type: Boolean,
      default: false,
    },
    idx: {
      type: Number,
    },
    qCurrent: Number
  },
  data() {
    return {
      checked: this.selected
    };
  },
  methods: {
    updateInput(e) {
      
      let key = e.target.value
      let value = e.target.checked
      console.log(e, key, value);
      this.$emit('picked', [key,value])
    },
  },
  watch: {
      qCurrent(newValue, oldValue) {
          this.checked = this.selected
      }
  },
};
</script>

<style scoped>
li {
  font-size: 20px;
  height: 30px;
}
</style>
