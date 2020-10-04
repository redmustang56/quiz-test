<template>
    <form class="form-l" @submit.prevent="eventHandler">
        <div class="form-l__tp">
            <svg-icon class="i-icon" name="form"></svg-icon>
            <div class="form-l__bl form-l__bl--fd">
                <div class="form-l__title">Кредитные и лизинговые программы</div>
                <div class="form-l__subtitle">Срок рассмотрения 1 час</div>
            </div>
        </div>
        <div class="form-l__nav">
            <a href="#" class="active">Условия кредитования</a>
            <a href="#">Условия лизинга</a>
        </div>
        <div class="form-l__bl form-l__bl--pb">
            <div class="input-field input-field--fw">
                <input
                        type="text"
                        v-model.number="month"
                />
                <label class="input-field__label" :class="month <= 0 ? '' : 'active'">Срок кредита, месяцев</label>
                <no-ssr>
                    <range-slider
                            class="slider"
                            min="10"
                            max="1000"
                            step="10"
                            v-model="month">
                    </range-slider>
                </no-ssr>
            </div>
            <div class="input-field input-field--fw">
                <input
                        type="text"
                        v-model.number="sumCredit"
                />
                <label class="input-field__label" :class="sumCredit <= 0 ? '' : 'active'">Сумма кредита</label>
                <no-ssr>
                    <range-slider
                            class="slider"
                            min="10"
                            max="10000000"
                            step="10"
                            v-model="sumCredit">
                    </range-slider>
                </no-ssr>
            </div>
        </div>
        <div class="form-l__bl form-l__bl--mb30 form-l__bl--wr">
            <div class="form-l__res">
                <span>Первоначальный взнос</span>
                <span>от 200 000 ₽</span>
            </div>
            <div class="form-l__res">
                <span>Ежемесячный платеж</span>
                <span>от 68 900 ₽</span>
            </div>
            <div class="form-l__res">
                <span>Процентная ставка</span>
                <span>от 8,8% ₽</span>
            </div>
        </div>
        <div class="form-l__bl form-l__bl--mb20">
            <div class="input-field input-field--mb">
                <input
                        type="text"
                        v-model="name"
                />
                <label class="input-field__label" :class="name <= 0 ? '' : 'active'">Имя</label>
            </div>
            <div class="input-field">
                <input
                        type="text"
                        v-model="phone"
                />
                <label class="input-field__label" :class="phone <= 0 ? '' : 'active'">Телефон</label>
            </div>
        </div>
        <div class="form-l__bl form-l__bl--alc">
            <p>Нажимая на кнопку «Отправить заявку» вы соглашаетесь с <n-link to="/">пользовательским соглашением</n-link>, <n-link to="/">положением о конфиденциальности</n-link> и <n-link to="/">офертой</n-link></p>
            <button class="btn" type="submit">Отправить заявку</button>
        </div>
    </form>
</template>

<script>
    import RangeSlider from 'vue-range-slider'
    import 'vue-range-slider/dist/vue-range-slider.css'

    export default {
        name: "form.vue",
        data: () => ({
            month: '48 мес',
            sumCredit: '980 000 ₽',
            name: '',
            phone: '',
        }),
        components: {
            RangeSlider
        },
        methods: {
            eventHandler() {

            }
        }
    }
</script>

<style src="~/assets/styles/css/global-styles/input.css" scoped />

<style lang="postcss" scoped>
    .form-l {
        background: #EFECE7;
        border: 1px solid #EFECE7;
        border-radius: 6px;
        padding: 30px;
        max-width: 920px;
        margin: 0 auto;

        @media(max-width: 1440px) {
            max-width: 780px;
        }
        @media(max-width: 1024px) {
            max-width: 550px;
        }
        @media(--max767) {
            max-width: initial;
            padding: 30px 22px;
            border-radius: 0;
        }

        &__tp {
            display: flex;
            align-items: center;
            margin-bottom: 30px;

            .i-icon {
                width: 36px;
                min-width: 36px;
                height: 36px;
                margin-right: 20px;
            }
        }
        &__title {
            font-weight: 500;
            font-size: 28px;
            line-height: 28px;

            @media(max-width: 470px) {
                font-size: 20px;
                line-height: 20px;
            }
        }
        &__subtitle {
            font-size: 20px;
            line-height: 24px;
            color: #003469;
            @media(max-width: 470px) {
                font-size: 16px;
                line-height: 20px;
            }

        }
        &__nav {
            margin-bottom: 60px;
            a {
                font-size: 20px;
                line-height: 24px;
                color: #767676;
                margin-right: 30px;

                &.active {
                    color: #00AAD2;
                }
                &:last-of-type {
                    margin-right: 0;
                }
            }
        }
        &__bl {
           display: flex;
            @media(max-width: 1024px) {
                flex-direction: column;
            }
            &--pb {
                padding-bottom: 44px;
                margin-bottom: 30px;
                border-bottom: 1px solid #E4DCD3;
            }
            &--mb30 {
                margin-bottom: 30px;
            }
            &--mb20 {
                margin-bottom: 20px;
            }
            &--fd {
                flex-direction: column;
            }
            &--wr {
                @media(max-width: 1024px) {
                    flex-direction: row;
                }
                @media(--max767) {
                    flex-direction: column;
                }
            }
            &--alc {
                @media(max-width: 1024px) {
                    align-items: center;
                }
            }
            p {
                max-width: 567px;
                margin-right: 20px;
                font-size: 12px;
                line-height: 14px;
                color: #767676;

                @media(max-width: 1440px) {
                    max-width: 350px;
                }
                @media(max-width: 1024px) {
                    order: 2;
                    max-width: initial;
                }

                a {
                    color: #00AAD2;
                    text-decoration: underline;
                }
            }
            .btn {
                margin-bottom: 20px;
            }
        }
        &__res {
            display: flex;
            flex-direction: column;
            margin-right: 20px;

            @media(--max767) {
                flex-direction: row;
                justify-content: space-between;
                margin-right: 0;
                margin-bottom: 17px;
            }

            &:last-of-type {
                margin-right: 0;
                @media(--max767) {
                    margin-bottom: 0;
                }
            }

            span {

                &:first-of-type {
                    display: block;
                    line-height: 17px;
                    margin-bottom: 5px;
                }
                &:last-of-type {
                    font-weight: 500;
                    font-size: 18px;
                    line-height: 18px;
                }
            }
        }
        .input-field {
            margin-left: 20px;
            width: 50%;

            &:first-of-type {
                margin-left: 0;
            }

            @media(max-width: 1024px) {
                width: 100%;
                margin-left: 0;
            }
            &--fw {
                &:first-of-type {
                    @media(max-width: 1024px) {
                        margin-bottom: 64px;
                    }
                }
                .input-field__label {
                    &.active {
                        color: #1B1B1B;
                        font-weight: 500;
                        font-size: 16px;
                    }
                }
            }
            &--mb {
                @media(max-width: 1024px) {
                    margin-bottom: 20px;
                }
            }
        }
    }
    .btn {
        margin: 0;
        display: inline-block;
        background: #00AAD2;
        border-radius: 6px;
        font-weight: 500;
        font-size: 15px;
        line-height: 15px;
        text-align: center;
        color: #F6F3F2;
        padding: 17px 72px;

        @media(max-width: 1440px) {
            width: 50%;
            max-width: 350px;
        }
        @media(max-width: 1024px) {
            width: 100%;
        }
        @media(max-width: 380px) {
            width: 100%;
            max-width: initial;
        }
    }

</style>

<style lang="postcss">
    .range-slider {
        position: absolute;
        left: 0;
        bottom: -10px;
        width: 100%;
        padding: 0;
        &-rail {
            background: transparent;
        }
        &-fill {
            background: #00AAD2;
        }
        &-knob {
            &:after {
                content: '';
                position: absolute;
                top: 4px;
                left: 4px;
                width: 10px;
                height: 10px;
                border-radius: 50%;
                background: #00AAD2;
            }
        }
    }
</style>
