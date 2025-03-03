<template>
    <div>
        <h1>{{ quiz.title }}</h1>
        <Progress :value="step" :max="quiz.questions.length - 1"/>
        <Question :question="question" v-if="question" @answer="addAnswer"/>
        {{ answers }}
    </div>
</template>

<script setup>
    import { computed, ref } from 'vue'
    import Progress from './Progress.vue';
    import Question from './Question.vue';

    const props = defineProps({
        quiz: Object
    })

    const state = red('question')
    const answers = ref(props.quiz.questions.map(() => null))
    const step = ref(0)
    const question = computed(() => props.quiz.questions[step.value])
    const addAnswer = (answer) => {
        answer.value[step.value] = answer
        step.value++
    }
</script>