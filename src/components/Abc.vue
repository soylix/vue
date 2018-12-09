<template>
    <h1>{{ msg1 }}</h1>
</template>

<script>
export default {
  name: 'abc',
  data () {
    return {
      msg1: '这是Abc页面'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1{
  font-weight: normal;
}

</style>
