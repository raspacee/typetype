<template>
  <div class="banner">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
export default {
  name: 'Banner',
  props: {
    msg: String
  }
}
</script>

<style scoped>

h1{
  font-size: 44px;
  background-color: #5cb85c;
  padding: 15px 0;
  color: white;
}
</style>
