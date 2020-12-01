<template>
  <div class="container">
    <div class="jumbotron question__box">
      <p class="lead question">
        {{ currentQuestion.question }}
      </p>
      <hr class="my-4" />

      <ul class="list-group m-auto">
        <li
          v-for="(answer, index) in shuffledAnswers"
          :key="index"
          class="list-group-item"
          @click="selectAnswer(index)"
          :class="answerClass(index)">
          {{ answer }}
        </li>
      </ul>

      <div class="answer__btn">
        <a
        class="btn btn-md"
        role="btn"
        @click="submitAnswer"
        :class="[selectedIndex === null ? 'unclickale' : '']"
      >
        Submit 🆗
      </a>
      <a class="btn btn-md" role="button" @click="next">
        Next ➡️ 
      </a>
      </div>
    </div>
  </div>
</template>

<script>
import _ from "lodash";

export default {
  name: "QuestionBox",
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function,
    index: Number
  },
  data() {
    return {
      selectedIndex: null,
      correctIndex: null,
      shuffledAnswers: [],
      answered: false,
    };
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
      return answers
    },
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null
        this.answered = false
        this.shuffleAnswers()
      },
    },
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index
    },
    shuffleAnswers() {
      let answers = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer,
      ]
      this.shuffledAnswers = _.shuffle(answers)
      this.correctIndex = this.shuffledAnswers.indexOf(
        this.currentQuestion.correct_answer
      )
    },
    submitAnswer() {
      let isCorrect = false

      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true
      }

      this.answered = true

      this.increment(isCorrect)
    },
    answerClass(index) {
      let answerClass = ''

      if (!this.answered && this.selectedIndex === index) {
        answerClass = 'selected'
      } else if (this.answered && this.correctIndex === index) {
        answerClass = 'correct'
      } else if (this.answered && this.selectedIndex === index && this.correctIndex !== index) {
        answerClass = 'incorrect'
      }

      return answerClass
    }
  }
}
</script>

<style scoped>
.question {
  color: #f2f2f2;
  font-size: 21px;
  font-weight: 700;
}

.question__box {
  margin-top: 50px;
  background-color: #80BF9B;
}

.list-group {
  border: 1px solid #025940;
  width: 90%;
}

.list-group li {
  font-weight: 500;
}

.list-group-item:hover {
  background: #d9d9d9;
  cursor: pointer;
}

.answer__btn {
  margin-top: 25px;
}

.btn {
  margin: 0 20px;
  background-color: #025940;
  color: #f2f2f2;
}

.btn:hover {
  color: #F26052;
}

.selected {
  background-color: #29a7d9a9;
  pointer-events: none;
}

.correct {
  background-color: #8fd9b6;
  pointer-events: none;
}

.incorrect {
  background-color: #F26052;
  pointer-events: none;
}

.unclickale {
  opacity: 0.5;
  pointer-events: none;
}


@media (max-width: 325px) {
  .btn {
    margin: 10px 10px;
  }
}
</style>
