<template>
  <div class="exam-result">
    <h2>Exam Finished</h2>
    <p>Your Score: {{ score }} / 100</p>
  </div>
</template>

<script>
export default {
  name: 'ExamResult',
  props: ['score']
};
</script>

<style scoped>
.exam-result {
  text-align: center;
  margin-top: 50px;
  background-color: #ffe6f2; /* Soft pink background */
  padding: 40px;
  border-radius: 20px;
  color: #5a2d82; /* Rich purple text */
  animation: fadeIn 1.5s ease-in-out;
  box-shadow: 0px 5px 15px rgba(255, 182, 193, 0.4); /* Light pink shadow */
}

h2 {
  font-size: 2.5em;
  color: #ff69b4; /* Hot pink for the heading */
  margin-bottom: 20px;
  animation: popIn 1s ease;
}

p {
  font-size: 1.5em;
  color: #ff8da1; /* Soft coral pink for the score */
  animation: bounceIn 2s ease;
}

/* Animations */
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes popIn {
  from {
    transform: scale(0.7);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
  }
}

@keyframes bounceIn {
  0% {
    transform: translateY(-20px);
    opacity: 0;
  }
  50% {
    transform: translateY(10px);
    opacity: 0.5;
  }
  100% {
    transform: translateY(0);
    opacity: 1;
  }
}
</style>