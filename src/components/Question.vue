<template>
    <div class="question">
        <h3>{{ question.question }}</h3>
        <ul>
            <li v-for="(choice, index) in randomChoices" :key="choice">
                <Answer 
                    :id="`answer${index}`"
                    :disabled="hasAnswer"
                    :value="choice"
                    @change="onAnswer"
                    v-model="answer"
                    :correctAnswer="question.correct_answer"
                />
            </li>
        </ul>
        <!-- <button :disabled="!hasAnswer" @click="emits('answer', answer)">Question suivante</button> -->
    </div>
</template>

<script setup>
    import { shuffleArray } from '@/functions/array'
    import { computed, onMounted, onUnmounted, ref } from 'vue'
    import Answer from './Answer.vue'

    const props = defineProps({
        question: Object
    })
    const emits = defineEmits(['answer'])
    const answer = ref(null)
    const hasAnswer = computed(() => answer.value !== null)
    const randomChoices = computed(() => shuffleArray(props.question.choices))
    let timer 

    const onAnswer = () => {
        clearTimeout(timer)
        timer = setTimeout(() => {
            emits('answer', answer.value)
        }, 1500)
    }
    

    onMounted(() => {
        timer = setTimeout(() => {
            answer.value = ''
            onAnswer()
        }, 3000)
    })

    onUnmounted(() => {
        clearTimeout(timer)
    })
</script>

<style>
    .question {
        padding-top: 2rem;
        & button {
            margin-left: auto;
            display: block;
        }
    }


</style>