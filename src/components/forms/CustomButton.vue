<template lang="pug">
.custom-button
  button(
    @click="onClick"
  )
    | {{ text }}
</template>

<script>
export default {
  name: 'CustomButton',

  props: {
    text: {
      type: String,
      required: true
    }
  },

  methods: {
    onClick() {
      this.$emit('on-click')
    }
  }
}
</script>