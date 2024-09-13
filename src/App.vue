<template>
  <div id="app" class="futuristic-container">
    <h1 class="title">Computer Basics Test</h1>
    <p>Hello Aasia 👋👋🎉✨❤💕👋💕. Here Are Your Test Instructions</p>
    <p>You have 2 hours to complete the test</p>
    <p>Each Question holds a point (1) as a mark</p>
    <p>Answer as many as possible</p>
    <p>Goodluck😋😋😋😋</p>
    <p>Don't Cry 😜😜</p>
    <ExamStart v-if="!examStarted" @start-exam="startExam" />
    <ExamQuestions 
      v-else-if="!examFinished"
      :questions="questions"
      :time-remaining="timeRemaining"
      :user-answers="userAnswers"
      @update-answer="updateAnswer"
      @submit-exam="submitExam"
    />
    <ExamResult v-else :score="score" />
  </div>
</template>

<script>
import ExamStart from './components/ExamStart.vue';
import ExamQuestions from './components/ExamQuestions.vue';
import ExamResult from './components/ExamResult.vue';
import { questions } from './data/questions';

export default {
  name: 'App',
  components: {
    ExamStart,
    ExamQuestions,
    ExamResult
  },
  data() {
    return {
      examStarted: false,
      examFinished: false,
      timeRemaining: 7200, // 2 hours in seconds
      questions,
      userAnswers: Array(questions.length).fill(null),
      score: 0,
      timer: null
    };
  },
  methods: {
    startExam() {
      this.examStarted = true;
      this.timer = setInterval(this.updateTimer, 1000);
    },
    updateTimer() {
      if (this.timeRemaining > 0) {
        this.timeRemaining--;
      } else {
        this.submitExam();
      }
    },
    updateAnswer(index, answer) {
      this.userAnswers.splice(index, 1, answer); // Directly update the array
    },
    submitExam() {
      clearInterval(this.timer);
      this.examFinished = true;
      this.calculateScore();
    },
    calculateScore() {
      this.score = this.questions.reduce((total, question, index) => {
        return total + (this.userAnswers[index] === question.correctAnswer ? 1 : 0);
      }, 0);
    }
  }
};
</script>

<style>
#app {
  font-family: 'Arial', cursive, sans-serif;
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f9e3e9; /* Soft pink background */
  border-radius: 20px;
  box-shadow: 0 8px 16px rgba(255, 182, 193, 0.4);
}

h1 {
  color: #d81b60; /* Dark feminine pink */
  text-align: center;
  font-size: 2.8em;
  margin-bottom: 30px;
  animation: bounceIn 1.5s ease;
}

@keyframes bounceIn {
  0% {
    transform: translateY(-30px);
    opacity: 0;
  }
  50% {
    transform: translateY(10px);
    opacity: 0.8;
  }
  100% {
    transform: translateY(0);
    opacity: 1;
  }
}
</style>
