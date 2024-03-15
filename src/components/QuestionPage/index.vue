<template>
    <div class="question-page">
        <h2 class="question-page___question">{{question.title}}</h2>
        <div class="question-page__answers">
            <div 
                v-for="item in question.answerList"
                :key="item.id"
                :class="[currentAnswer?.id === item.id ? 'active' : '', 'question-page__item']"
                @click="setAnswer(item)"
            >- {{item.text}}</div>
        </div>
        <h2 v-if="currentAnswer">Текущий ответ: {{currentAnswer.text}}</h2>
        <h2 v-else>Ответ пока не выбран</h2>
        <div
            class="button"
            @click="goToNextQuestion()"
        >Далее</div>
    </div>
</template>

<script>
export default {
    name: 'QuestionPage',
    props: {
        question: {
            type: Object,
            required: true,
        }
    },
    data() {
        return {
            currentAnswer: null,
        }
    },
    methods: {
        setAnswer(item) {
            this.currentAnswer = item;
        },
        goToNextQuestion() {
            this.$emit('nextQuestion', this.currentAnswer);
            this.currentAnswer = null;
        }
    }
}
</script>

<style lang="scss">
    .question-page {
        display: flex;
        flex-direction: column;
        align-items: center;

        &__answers {
            display: flex;
            flex-direction: column;
            align-items: flex-start;
            width: fit-content;
            margin: 40px 0;
        }

        &__item {
            cursor: pointer;
            text-align: left;
            padding: 10px;
            width: 100%;
            font-size: 18px;
            transition: .3s;

            &.active {
                color: rgb(10, 155, 39);
            }

            &:hover {
                transform: scale(1.05);
            }

            &:active {
                transform: scale(0.95);
            }
        }
    }

    .button {
        width: fit-content;
        cursor: pointer;
        margin-top: 40px;
        padding: 12px 32px;
        background-color: rgba(211, 211, 211, .5);
        border-radius: 3px;
        font-size: 20px;
        transition: .3s;

        &:hover {
            background-color: rgba(211, 211, 211, .7);
        }
    }
</style>
