<template>
  <div id="app">
    <!-- The header component -->
    <Header :numCorrect="numCorrect" />

    <!-- The questions box component -->
    <QuestionBox
      v-if="questions.length"
      :currentQuestion="questions[index]"
      :next="next"
      :increment="increment"
    />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";

export default {
  name: "App",
  components: {
    Header,
    QuestionBox,
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
    };
  },
  methods: {
    next() {
      if (this.index == 10) {
        alert(`You have ${this.numCorrect} correct answer`)
      } else {
        this.index++;
      }
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++;
      }
    },
  },
  mounted() {
    fetch(
      "https://opentdb.com/api.php?amount=10&category=17&difficulty=easy&type=multiple",
      {
        method: "get",
      }
    )
      .then((response) => {
        return response.json();
      })
      .then((jsonData) => {
        this.questions = jsonData.results;
      });
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html, body {
  background-color: #F2D1C9;
}

#app {
  font-family: 'Poppins', sans-serif;
  text-align: center;
  background-color: #F2D1C9;
  color: #000000;
}
</style>
