<template>
  <Banner msg="TypeType"/>

  <ParagraphBox :paragraph="paragraph"/>

  <TypingBox :paragraph="paragraph" v-on:fetch-paragraph="fetchParagraph"/>

  <Footer/>
</template>

<script>
import Banner from './components/Banner.vue'
import ParagraphBox from './components/ParagraphBox.vue'
import TypingBox from './components/TypingBox.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Banner,
    ParagraphBox,
    TypingBox,
    Footer
  },
  data() {
    return {
      paragraph: '',
      paragraph_count: 1,
    }
  },
  methods: {
    async fetchParagraph() {
      const response = await fetch(`https://baconipsum.com/api/?type=meat-and-filler&paras=${this.paragraph_count}&format=text`);
      const data = await response.text();
      if (data) {
        this.paragraph = data;
      }
    }
  },
  created() {
    this.fetchParagraph();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}
</style>
