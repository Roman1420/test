<template>
    <question-page
        v-if="!showFinalPage"
        :question="getCurrentQuestion"
        @nextQuestion="setNextQuestion"
    />
    <final-page
        v-else
        :answers="answers"
    />

</template>

<script>
import QuestionPage from './components/QuestionPage/index.vue'
import FinalPage from './components/FinalPage/index.vue'
import questions from './questions.js'

export default {
    name: 'App',
    components: {
        QuestionPage,
        FinalPage
    },
    data() {
        return {
            questions: questions,
            answers: [],
            currentQuestionId: 0,
            showFinalPage: false
        }
    },
    methods: {
        setNextQuestion(answer) {
            console.log('answer: ', answer);
            this.answers.push(
                {
                    questionId: this.currentQuestionId,
                    answerId: answer?.id ?? null
                }
            );
            
            const testIsFinished = this.answers.length === this.questions.length;
            if (testIsFinished) {
                this.showFinalPage = true;
            } else {
                this.currentQuestionId++;
            }
            console.log('answers: ', this.answers);
        },
    },
    computed: {
        getCurrentQuestion() {
            const currentQuestion = this.questions.find(question => question.id === this.currentQuestionId);
            return currentQuestion ?? null;
        }
    }
}
</script>

<style>
* {
    margin: 0;
    box-sizing: border-box;
}

#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    overflow: hidden;
}
</style>
