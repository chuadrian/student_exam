<template>
    <div class="exam-start">
      <button @click="$emit('start-exam')" class="futuristic-button">Start Exam</button>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ExamStart'
  };
  </script>
  
  <style scoped>
.exam-start {
  text-align: center;
  margin-top: 50px;
}

button {
  font-size: 1.5em;
  padding: 15px 30px;
  background-color: #ff85a2; 
  color: #fff;
  border: none;
  border-radius: 30px;
  cursor: pointer;
  box-shadow: 0 8px 16px rgba(255, 133, 162, 0.4);
  transition: transform 0.3s;
}

button:hover {
  transform: scale(1.05); /* Playful hover effect */
}

button:active {
  transform: scale(0.98);
}
</style>