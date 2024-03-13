<template>
    <question-page
        :question="getCurrentQuestion"
        @nextQuestion="setNextQuestion"
    />
</template>

<script>
import QuestionPage from './components/QuestionPage/index.vue'
import questions from './questions.js'

export default {
    name: 'App',
    components: {
        QuestionPage
    },
    data() {
        return {
            questions: questions,
            answers: [],
            currentQuestionId: 0,
        }
    },
    methods: {
        setNextQuestion(answer) {
            console.log('answer: ', answer);
            this.answers.push({
                questionId: this.currentQuestionId,
                answerId: answer?.id
            });
            this.currentQuestionId++;
            console.log('answers: ', this.answers);
            //... менять вопрос
        },
    },
    computed: {
        getCurrentQuestion() {
            return this.questions.find(question => question.id === this.currentQuestionId)
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
