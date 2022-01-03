<template>
  <div
    class="li-wrapper"
    :style="{
      '--columns-count': this.columnsCount,
      background: isActive ? 'lightgreen' : 'white'
    }"
    @click="$emit('component-clicked')"
  >
    {{ title }}
  </div>
</template>

<script>
export default {

  name: "TabElement",
  props:{
    title:{
      default: '',
      type: String,
    },
    columnsCount:{
      default: 3,
      type: Number,
    },
    isActive:{
      default: false,
      type: Boolean,
    }
  },
}
</script>

<style scoped lang="scss">
li{
  margin: 0;
  padding: 0;
}
.li-wrapper{
  width: calc(100% / var(--columns-count) - 52px );
  padding: 20px;
  overflow-wrap: break-word;
  height: fit-content;
  border: 1px solid black;
  background: white;
  margin: 5px;
}
</style>