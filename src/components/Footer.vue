<template>
  <div class="footer">
    <p class="footer-text-left">
      Made with <span style="color: #e25555;">&#9829;</span> in my garage.
    </p>
  </div>
</template>

<script>
export default {
  name: 'Footer',
  data () {
    return {

    }
  }
}
</script>

<style lang="css" scoped>
.footer {
  position:fixed;
  bottom:0;
  left:0;
  width:100%;
  height: 50px;
  background-color: #D0DAEE;
}

.footer-text-left {
  font-size:18px;
  padding-left:40px;
  float:left;
}
</style>