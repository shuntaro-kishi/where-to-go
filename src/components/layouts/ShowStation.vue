<template lang="pug">
.show-station
  .start-message(
    v-if="randomIndex === -1"
  )
    | 行き先を決めましょう
  .station-text(
    v-else
  )
    | {{ stations[randomIndex] }}
</template>

<script>
export default {
  name: 'ShowStation',

  props: {
    stations: {
      type: Array,
      required: true
    },
    randomIndex: {
      type: Number,
      required: true
    }
  }
};
</script>

<style lang="scss" scoped>
.show-station {
  font-size: 200px;
}
</style>