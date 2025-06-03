<template>
  <div class="container">
    <div class="header">{{ header }}</div>

    <div class="content">
      <slot name="content"></slot>
    </div>

    <div class="footer">
      <slot name="footer"></slot>
    </div>
  </div>
</template>

<script> 

export default {
  name: 'TComponent',
  props: {
    header: String
  }
}


</script>

<style lang="stylus">
.container
  width: 300px
  height: 400px
  border: 1px solid black
  display: flex
  flex-direction: column

.header
  background: yellow
  flex-basis: 100px
.content
  background: lightpink
  flex-basis: 200px
.footer
  background: lightblue
  flex-basis: 100px


</style>