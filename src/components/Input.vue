<template>
  <fieldset class="c-fieldset">
    <label class="c-label">{{ label }}</label>
    <input 
      v-bind:value="value"
      v-on:input="$emit('input', $event.target.value)"
      class="c-input"
      :type="type"
      :placeholder="placeholder" 
      :minlength="minlength" />
  </fieldset>
</template>

<script>
export default {
  name: "Input",
  props: {
    value: String,
    type: String,
    placeholder: String,
    label: String,
    minlength: Number
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.c-fieldset {
  display: block;
  text-align: left;
  border: 0;
  .c-label {
    display: block;
    margin-bottom: 0.25rem;
  }
  .c-input {
    padding: 0.5rem 0.75rem;
    width: 100%;
    border: 1px solid #ccc;
    &:focus {
      border: 1px solid blue;
      outline: 0;
    }
  }
}
</style>
