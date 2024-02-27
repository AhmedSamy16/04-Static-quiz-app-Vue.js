<template>
  <div class="app">
    <div class="score-section" v-if="showScore">
      You Scored {{ score }} out of {{ length }}
      <button @click="reset">Reset</button>
    </div>
    <template v-else>
      <div class="question-section">
        <div class="question-count">
          <span>Question {{ currentIndex + 1 }}</span>/{{ length }}
        </div>
        <div class="question-text">{{ question.questionText }}</div>
      </div>
      <div class="answer-section">
        <button v-for="answer in question.answerOptions" @click="handleAnswer(answer.isCorrect)">{{ answer.answerText }}</button>
      </div>
    </template>
  </div>
</template>

<script lang="ts">
  const questions = [
		{
			questionText: 'What is the capital of France?',
			answerOptions: [
				{ answerText: 'New York', isCorrect: false },
				{ answerText: 'London', isCorrect: false },
				{ answerText: 'Paris', isCorrect: true },
				{ answerText: 'Dublin', isCorrect: false },
			],
		},
		{
			questionText: 'Who is CEO of Tesla?',
			answerOptions: [
				{ answerText: 'Jeff Bezos', isCorrect: false },
				{ answerText: 'Elon Musk', isCorrect: true },
				{ answerText: 'Bill Gates', isCorrect: false },
				{ answerText: 'Tony Stark', isCorrect: false },
			],
		},
		{
			questionText: 'The iPhone was created by which company?',
			answerOptions: [
				{ answerText: 'Apple', isCorrect: true },
				{ answerText: 'Intel', isCorrect: false },
				{ answerText: 'Amazon', isCorrect: false },
				{ answerText: 'Microsoft', isCorrect: false },
			],
		},
		{
			questionText: 'How many Harry Potter books are there?',
			answerOptions: [
				{ answerText: '1', isCorrect: false },
				{ answerText: '4', isCorrect: false },
				{ answerText: '6', isCorrect: false },
				{ answerText: '7', isCorrect: true },
			],
		},
	];
  export default {
    data() {
      return {
        currentIndex: 0,
        showScore: false,
        score: 0,
        length: questions.length
      }
    },
    computed: {
      question() {
        return questions[this.currentIndex]
      }
    },
    methods: {
      handleAnswer(isCorrect: boolean) {
        if (isCorrect) {
          this.score++
        }
        if (this.currentIndex + 1 < questions.length) {
          this.currentIndex++
        } else {
          this.showScore = true
        }
      },
      reset() {
        this.currentIndex = 0
        this.showScore = false
        this.score = 0
      }
    }
  }
</script>

<style>
body {
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #7cc6fe;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

* {
  color: #fff;
}

.app {
  background-color: #252d4a;
  width: 450px;
  min-height: 200px;
  height: min-content;
  border-radius: 15px;
  padding: 20px;
  box-shadow: 10px 10px 42px 0px rgba(0, 0, 0, 0.75);
  display: flex;
  justify-content: space-evenly;
}

.score-section {
  display: flex;
  flex-direction: column;
  font-size: 24px;
  justify-content: space-between;
  align-items: center;
  padding: 25px 0;
}

.question-section {
  width: 100%;
  position: relative;
}

.question-count {
  margin-bottom: 20px;
}

.question-count span {
  font-size: 28px;
}

.question-text {
  margin-bottom: 12px;
}

.answer-section {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

button {
  width: 100%;
  font-size: 16px;
  color: #fff;
  background-color: #252d4a;
  border-radius: 15px;
  display: flex;
  padding: 5px;
  justify-content: center;
  align-items: center;
  border: 5px solid #234668;
  cursor: pointer;
  transition: all 0.3s ease-out;
}

button:hover {
  background-color: #555e7d;
}
</style>