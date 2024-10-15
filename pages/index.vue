<template>
  <div class="h-[calc(100vh)] bg-[hsl(275,100%,97%)] flex flex-col items-center">
    <div>
      <img v-if="isMobile" src="/images/background-pattern-mobile.svg" alt="Background Pattern Mobile">
      <img v-else src="/images/background-pattern-desktop.svg" alt="Background Pattern Desktop">
    </div>
    <div class="bg-[hsl(0,0%,100%)] rounded-lg w-[87%] h-[65%] mt-[-90px] shadow-lg flex flex-col p-7 md:w-[42%] md:rounded-3xlg">
      <div class="flex w-[100%] pb-3">
        <img class="w-[23px] md:w-[40px]" src="/images/icon-star.svg" alt="Icon Star">
        <h1 class="font-[700] text-[hsl(292,42%,14%)] text-[32px] ml-[18px] md:text-[50px]">
          FAQs
        </h1>
      </div>

      <div v-for="(question, index) in questions" :key="index">
        <div class="flex justify-between mb-5 cursor-pointer" @click="() => toggleAnswer(index)">
          <h1 class="text-[hsl(292,42%,14%)] font-[600] leading-5 w-[230px] hover:text-[#A53CD6] md:w-full md:text-[18px]">
            {{ question.title }}
          </h1>
          <a class="flex justify-center items-center h-full">
            <img :src="showAnswers[index] ? '/images/icon-minus.svg' : '/images/icon-plus.svg'" alt="Toggle Icon">
          </a>
        </div>
        <p v-if="showAnswers[index]" class="text-[hsl(292,16%,49%)] text-[14px] mb-5 md:text-[16px]">
          {{ question.answer }}
        </p>
        <hr class="mb-5">
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

// Comportamento do accordion
const questions = [
  {
    title: 'What is Frontend Mentor, and how will it help me?',
    answer: "Frontend Mentor offers realistic coding challenges to help developers improve their frontend coding skills with projects in HTML, CSS, and JavaScript. It's suitable for all levels and ideal for portfolio building."
  },
  {
    title: 'Is Frontend Mentor free?',
    answer: 'Yes, Frontend Mentor offers both free and premium coding challenges. The free tier provides access to a wide range of projects suitable for all skill levels.'
  },
  {
    title: 'Can I use Frontend Mentor projects in my portfolio?',
    answer: "Absolutely! You can use projects you've completed on Frontend Mentor in your portfolio. It's a great way to showcase your skills to potential employers."
  },
  {
    title: "How can I get help if I'm stuck on a challenge?",
    answer: 'Frontend Mentor has a supportive community. You can ask for help in the community forum, or join their Discord server to connect with other developers and get assistance.'
  }
]
const showAnswers = ref(new Array(questions.length).fill(false))
const toggleAnswer = (index: number) => {
  showAnswers.value = showAnswers.value.map((value, i) => i === index ? !value : false)
}

// Comportamento da imagem atrás do card
const isMobile = ref(false)
const checkMediaQuery = () => {
  isMobile.value = window.matchMedia('(max-width: 375px)').matches
}
onMounted(() => {
  checkMediaQuery()
  window.addEventListener('resize', checkMediaQuery)
})
onBeforeUnmount(() => {
  window.removeEventListener('resize', checkMediaQuery)
})
</script>
