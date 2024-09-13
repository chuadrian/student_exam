<template>
    <div class="exam-questions">
      <h2 class="time-remaining">Time Remaining: {{ formatTime(timeRemaining) }}</h2>
      <div v-for="(question, index) in questions" :key="index" class="question">
        <h3>Question {{ index + 1 }}</h3>
        <p>{{ question.text }}</p>
        <div v-for="(option, optionIndex) in question.options" :key="optionIndex" class="option">
          <input
            type="radio"
            :id="'q' + index + 'o' + optionIndex"
            :name="'question' + index"
            :value="optionIndex"
            v-model="localAnswers[index]"
            @change="updateAnswer(index, optionIndex)"
            class="radio-input"
          />
          <label :for="'q' + index + 'o' + optionIndex" class="option-label">{{ option }}</label>
        </div>
      </div>
      <button @click="$emit('submit-exam')" class="submit-button">Submit Exam</button>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ExamQuestions',
    props: ['questions', 'timeRemaining', 'userAnswers'],
    data() {
      return {
        localAnswers: [...this.userAnswers], // Create a local copy of userAnswers
      };
    },
    methods: {
      formatTime(seconds) {
        const minutes = Math.floor(seconds / 60);
        const remainingSeconds = seconds % 60;
        return `${minutes}:${remainingSeconds < 10 ? '0' : ''}${remainingSeconds}`;
      },
      updateAnswer(index, optionIndex) {
        this.localAnswers.splice(index, 1, optionIndex); // Directly update localAnswers
        this.$emit('update-answer', index, optionIndex); // Emit the update to the parent
      }
    },
    watch: {
      userAnswers: {
        handler(newValue) {
          this.localAnswers = [...newValue]; // Sync localAnswers with changes in the parent prop
        },
        deep: true
      }
    }
  };
  </script>
  
  <style scoped>
.exam-questions {
  margin-top: 20px;
  padding: 20px;
  background-color: #ffe6f2; /* Soft pink background */
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(255, 182, 193, 0.4);
}

h2 {
  font-size: 2em;
  color: #d81b60; /* Feminine dark pink */
}

.question {
  margin-bottom: 20px;
}

h3 {
  color: #f06292; /* Soft coral pink */
}

button {
  font-size: 1.5em;
  padding: 12px 25px;
  background-color: #ff85a2;
  color: #fff;
  border: none;
  border-radius: 30px;
  cursor: pointer;
  box-shadow: 0 8px 16px rgba(255, 133, 162, 0.4);
  transition: transform 0.3s;
}

button:hover {
  transform: scale(1.05);
}

button:active {
  transform: scale(0.98);
}

label {
  margin-left: 10px;
  color: #d81b60;
}
</style>