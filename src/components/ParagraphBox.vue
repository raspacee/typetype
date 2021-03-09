<template>
  <div class="paragraph-box">
    <code class="paragraph">
      <span v-for="(letter, idx) in paragraph" v-bind:key="idx" :data-idx="idx" >{{ letter }}</span>
    </code>
  </div>
</template>

<script>
export default {
  name: 'ParagraphBox',
  props: {
    paragraph: String
  },
  data () {
    return {
    }
  }
}
</script>

<style lang="css">

.paragraph-box {
    width: 60%;
    margin: 70px auto;
}

.paragraph {
    font-size: 24px;
}

.correct-letter {
  color: green;
}

.incorrect-letter {
  color: red;
}

.cursor {
  color: white;
  background-color: black;
}
</style>