<template>
  <div>
  <div class="typing-box">
    <input type="text" v-on:focus="pointCursor" v-on:input="handleTyping" name="current_letter" v-model="current_letter" placeholder="Start typing...">

    <!-- <button @click="reset" v-on:click="$emit('fetch-paragraph')">Reset</button> -->
    <button @click="reset" v-on:click="$emit('fetch-paragraph')" class="button"
      style="vertical-align:middle"><span>Reset</span></button>
  </div>

  <div id="myModal" class="modal">
    <!-- Modal content -->
    <div class="modal-content">
      <div class="modal-header">
        <h2>Result</h2>
      </div>
      <span v-on:click="closeModal" class="close">&times;</span>
      <h3>You typed <span class="correct-letter big-font">{{ correct_letter }}</span> out of <span class="big-font">{{ para_length }}</span> letters correctly.</h3>
      <h3><span class="incorrect-letter big-font">{{ incorrect_letter }}</span> were incorrect.</h3>
    </div>
  </div>
  </div>
</template>

<script>
export default {
  name: 'TypingBox',
  props: {
    paragraph: String,
    fetchParagraph: Function,
  },
  data () {
    return {
      current_letter: '',
      cl_index: 0,
      para_length: 0,
      correct_letter: 0,
      incorrect_letter: 0
    }
  },
  methods: {
    handleTyping() {
      this.para_length = this.paragraph.split('').length;

      if (this.cl_index < (this.para_length - 1)) {
        if (this.paragraph.split('')[this.cl_index] == this.current_letter) {
          document.querySelector(`[data-idx="${this.cl_index}"]`).classList.add('correct-letter')
          this.correct_letter++;
        } else {
          document.querySelector(`[data-idx="${this.cl_index}"]`).classList.add('incorrect-letter')
          this.incorrect_letter++;
        }
        this.current_letter = '';
        this.cl_index++;

        // increment the cursor
        if (this.cl_index < this.para_length){
          this.increment_cursor();
        }
      } else {
        document.getElementById('myModal').style.display = 'block';
      }
    },
    increment_cursor() {
      document.querySelector(`[data-idx="${this.cl_index - 1}"]`).classList.remove('cursor');
      document.querySelector(`[data-idx="${this.cl_index}"]`).classList.add('cursor');
    },
    reset() {
      this.current_letter = '';
      this.cl_index = 0;

      for (let i = 0; i < document.querySelectorAll('[data-idx]').length; i++) {
        document.querySelectorAll('[data-idx]')[i].classList = '';
      }
      document.querySelector('[data-idx="0"]').classList.add('cursor');
    },
    pointCursor() {
      if (this.cl_index == 0) {
        document.querySelector(`[data-idx="${this.cl_index}"]`).classList.add('cursor');
      }
    },
    closeModal() {
      document.getElementById("myModal").style.display = "none";
    }
  }
}
</script>

<style lang="css" scoped>
input[type=text] {
  outline: none;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  border: none;
  border-bottom: 2px solid black;
}

.big-font {
  font-size: 40px;
}

.modal {
  display: none; /* Hidden by default */
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0,0,0); /* Fallback color */
  background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
}

.modal-header {
  padding: 2px 16px;
  background-color: #5cb85c;
  color: white;
}

/* Modal Content/Box */
.modal-content {
  background-color: #fefefe;
  margin: 15% auto; /* 15% from the top and centered */
  padding: 20px;
  border: 1px solid #888;
  width: 80%; /* Could be more or less, depending on screen size */
}

/* The Close Button */
.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}

.button {
  display: inline-block;
  border-radius: 4px;
  background-color: grey;
  border: none;
  color: #FFFFFF;
  text-align: center;
  font-size: 28px;
  padding: 15px;
  width: 150px;
  transition: all 0.5s;
  cursor: pointer;
  margin: 5px;
}

.button span {
  cursor: pointer;
  display: inline-block;
  position: relative;
  transition: 0.5s;
}

.button span:after {
  content: '\00bb';
  position: absolute;
  opacity: 0;
  top: 0;
  right: -20px;
  transition: 0.5s;
}

.button:hover span {
  padding-right: 25px;
}

.button:hover span:after {
  opacity: 1;
  right: 0;
}
</style>