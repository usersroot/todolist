<template>
   <header class="bar bar-nav" id="#Tab">
      <a class="icon icon-left pull-left"></a>
      <a class="icon icon-edit pull-right" @click="changetextflag"></a>
      <h1 class="title">todolist</h1>
  </header>
</template>

<script>
export default {
  name: 'Tab',
  methods: {
    changetextflag() {
        this.$emit('changetext')
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">

</style>
