<template>
  <input v-bind="$attrs" v-model="internalValue" @input="updateValue"
    placeholder="Search using UserName e.g. torrenegra01" />
</template>
  
<script>
export default {
  name: 'CustomInput',
  props: {
    value: [String, Number],
  },
  data() {
    return {
      internalValue: this.value,
    };
  },
  methods: {
    updateValue(event) {
      this.internalValue = event.target.value;
      this.$emit('input', this.internalValue);
    },
  },
};
</script>

<style>
input {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 100%;
  height: 50px;
}
</style>