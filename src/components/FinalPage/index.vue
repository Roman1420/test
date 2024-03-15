<template>
    <div class="final-page">
        <h2>Конец теста</h2>
        <p>Правильных ответов: </p>
        <p>Неправильных ответов: </p>
        <div>Кол-во ответов: {{rightAnswers.length}}, Кол-во правильных ответов: {{rightAnswers.length}}, </div>
    </div>
</template>

<script>
import rightAnswers from '../../questions.js'
export default {
    name: 'FinalPage',
    props: {
        answers: {
            type: Array,
            required: true
        }
    },
    data() {
        return {
            rightAnswers: rightAnswers,
        }
    }
}
</script>

<style>

</style>
