<template>
  <div class="input">
    <p class="form-authorization__label">{{label}}</p>

    <input
        class="form-authorization__input"
        :placeholder="placeholder"
        :type="type"
        :value="modelValue"
        :class="{'form-authorization__input_error': !isValide}"
        @input="$emit('update:modelValue', $event.target.value)"
    />
  </div>
</template>

<script>

export default {
  name: 'Input',

  props: {
    label: {
      type: String,
      default: ""
    },

    type: {
      type: String,
      default: "text"
    },

    placeholder: {
      type: String,
      default: ""
    },

    modelValue: {
      type: String,
      default: ""
    },

    isValide: {
      type: Boolean,
      default: false,
    },
  },

  components: {

  }
}
</script>

<style>
.input {

}
</style>