<template>
    <div class="content">
        <h1>Quiz</h1>
        <div v-for="(question, index) in quiz.questions">
            <div class="qq" v-show="index === questionIndex">
                <div v-if="questionIndex === 0">
                    <div class="qq__t">{{ quiz.questions[0].text }}(Чтобы ответить правильно напишите 'верный')</div>
                    <div class="input-field">
                        <input
                                type="text"
                                v-model="answer"
                                required
                        />
                        <label class="input-field__label" :class="answer.length <= 0 ? '' : 'active'">Напишите ответ</label>
                    </div>
                </div>
                <div v-if="questionIndex === 1">
                    <div class="qq__t">{{ quiz.questions[1].text }}</div>
                    <div class="m-select">
                        <label class="m-select__label active">{{ quiz.questions[1].text }}</label>
                        <multiselect v-model="userAnswer[index]"
                                     :options="quiz.questions[1].responses"
                                     track-by="correct"
                                     value="correct"
                                     label="text"
                                     :searchable="false"
                                     :allow-empty="false"
                                     :show-labels="false"
                        ></multiselect>
                    </div>
                </div>
                <div v-if="questionIndex === 2">
                    <div class="qq__t">{{ quiz.questions[2].text }}</div>
                    <label class="qq__l" v-for="response in quiz.questions[2].responses">
                        <input type="radio"
                               :value="response.correct"
                               :name="index"
                               v-model="userAnswer[index]"> {{response.text}}
                    </label>
                </div>
                <div v-if="questionIndex === 3">
                    <popup
                            v-if="isInfoPopupVisible"
                            @closePopup="closePopup"
                    >
                        <div class="qq__popup">
                            <div class="qq__t">{{ quiz.questions[3].text }}</div>
                            <label class="qq__l" v-for="response in quiz.questions[3].responses">
                                <input type="radio"
                                       :value="response.correct"
                                       :name="index"
                                       v-model="userAnswer[index]"> {{response.text}}
                            </label>
                            <button @click="next">Ответить</button>
                        </div>
                    </popup>
                </div>
                <button v-if="questionIndex > 0" @click="prev">пред.</button>
                <button @click="next">след.</button>
            </div>
        </div>
        <div v-show="questionIndex === quiz.questions.length">
            <p>Результат: {{ result() }} / {{ quiz.questions.length }}</p>
        </div>
    </div>
</template>

<script>
    import Multiselect from 'vue-multiselect'
    import popup from '~/components/popup'

    const quiz = {
        questions: [
            {
                text: "Вопрос 1",
                responses: [
                    {text: 'Не верный', correct: false},
                    {text: 'Верный', correct: true},
                ]
            },
            {
                text: "Вопрос 2",
                responses: [
                    {text: 'Верный', correct: true},
                    {text: 'Не верный', correct: false},
                ]
            },
            {
                text: "Вопрос 3",
                responses: [
                    {text: 'Верный', correct: true},
                    {text: 'Не верный', correct: false},
                ]
            },
            {
                text: "Вопрос 4",
                responses: [
                    {text: 'Верный', correct: true},
                    {text: 'Не верный', correct: false},
                ]
            }
        ]
    };

    export default {
        name: "quiz",
        data: () => ({
            quiz: quiz,
            questionIndex: 0,
            userAnswer: [],
            answer: '',
            isInfoPopupVisible: false,
        }),
        components: {
            Multiselect,
            popup
        },
        methods: {
            closePopup() {
                this.isInfoPopupVisible = false
            },
            next() {
                this.questionIndex++
                this.questionIndex === 3 ? this.isInfoPopupVisible = true : this.isInfoPopupVisible = false
            },
            prev() {
                this.questionIndex--
            },
            result() {
                if(this.userAnswer.length !== 0) {
                    this.answer !== 'верный' ? this.userAnswer[0] = false : this.userAnswer[0] = true
                    if(this.userAnswer[1].correct === true) {
                        this.userAnswer[1] = true
                    } else if(this.userAnswer[1].correct === false) {
                        this.userAnswer[1] = false
                    }
                    return this.userAnswer.filter(function(val) { return val }).length;
                }
            },
        }
    }
</script>

<style src="~/assets/styles/css/global-styles/input.css" scoped />
<style src="~/assets/styles/css/global-styles/m-select.css" scoped />

<style lang="postcss" scoped>
    .content {
        max-width: 1200px;
        margin: 0 auto;

        h1 {
            margin-bottom: 30px;
        }
    }
    .qq {
        &__t {
            font-size: 20px;
            font-weight: 500;
            margin-bottom: 20px;
        }
        &__l {
            display: block;
            margin-bottom: 10px;
        }
        button {
            margin: 20px 0;
            display: inline-block;
            background: #00aad2;
            color: #fff;
            border-radius: 6px;
            font-weight: 500;
            font-size: 15px;
            line-height: 15px;
            padding: 10px;
            cursor: pointer;
        }
        &__popup {
            display: flex;
            flex-direction: column;

            button {
                margin-top: 30px;
            }
        }
    }
</style>