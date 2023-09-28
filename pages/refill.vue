<template>
    <div class="money">

        <div class="money__body">
            <div class="text-center">
                <h1>Пополнение баланса</h1>
            </div>
            <div class="type">
                <NuxtLink to="/refill">
                    Пополнение
                </NuxtLink>
                <NuxtLink to='/withdrawal'>
                    Вывод
                </NuxtLink>
            </div>

            <p>Порядок действий для пополнения баланса</p>
            <p>1. Подтвердите Ваше согласие с правилами нашей системы</p>

            <label class="custom-checkbox">
                <input type="checkbox">
                <p class="checkbox-text m-0">Я согласен с <NuxtLink to="/terms">пользовательским соглашением
                    </NuxtLink>
                    и <NuxtLink to="/polytics">политикой конфиденциальности</NuxtLink>
                </p>
            </label>

            <p>2. Введите сумму, на которую вы хотите пополнить личный счёт, и нажмите на кнопку «Пополнить». Вы будете
                переадресованы на сайт платёжной системы, где сможете завершить платёж.</p>

            <div class="input">
                <input type="number" name="count" id="count" placeholder="100 ₸" v-model="count">
                <button>Пополнить</button>
            </div>

            <div class="selects">
                <button @click="count = 100" :class="{ selected: count == 100 }">100 ₸</button>
                <button @click="count = 1000" :class="{ selected: count == 1000 }">1000 ₸</button>
                <button @click="count = 2000" :class="{ selected: count == 2000 }">2000 ₸</button>
                <button @click="count = 5000" :class="{ selected: count == 5000 }">5000 ₸</button>
                <button @click="count = 10000" :class="{ selected: count == 10000 }">10000 ₸</button>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            count: null,
        }
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Пополнение счета | MerchShop',
    ogTitle: 'Пополнение счета | MerchShop',
    description: 'Пополнение счета | MerchShop',
    ogDescription: 'Пополнение счета | MerchShop',
})
</script>
<style lang="scss" scoped>
.money {
    padding: 150px 0 60px;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;

    @media (max-width: 1024px) {
        padding: 150px 20px 60px;
    }

    .money__body {
        border: 2px solid #D2D2D2;
        background: #fff;
        padding: 30px;

        @media (max-width: 1024px) {
            padding: 20px 10px;
        }

        .selects {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 10px;
            margin-top: 20px;

            .selected {
                background: #000 !important;
                color: #fff !important;
            }

            button {
                // flex: 1;
                background: transparent;
                border: 2px solid #000;
                padding: 13px 15px;
                transition: all .3s ease;

                font-size: 20px;
                font-style: normal;
                font-weight: 400;
                line-height: normal;
                font-family: var(--int);
                color: #000;
            }
        }

        .input {
            display: flex;
            gap: 20px;

            input {
                flex: 1;
                max-width: 227px;
                border: 2px solid #000;
                background: transparent;
                padding: 12px;
                text-align: right;

                font-size: 20px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                color: #000;

                @media (max-width: 1024px) {
                    max-width: 155px;
                }
            }

            button {
                flex: 1;
                background: #000;
                padding: 12px 0;
                border: 0;

                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #fff;
            }
        }

        p,
        a {
            margin-bottom: 20px;
            font-size: 20px;
            font-style: normal;
            font-weight: 400;
            line-height: 130%;
            font-family: var(--int);
            color: #000;
            max-width: 535px;

            @media (max-width: 1024px) {
                font-size: 16px;
                margin-bottom: 10px;
            }
        }

        a {
            text-decoration: underline;
        }

        .type {
            display: flex;
            margin-bottom: 20px;

            @media (max-width: 1024px) {
                margin-bottom: 0;
            }

            a {
                flex: 1;
                padding: 12px;
                background: transparent;
                border: 2px solid #000;
                text-decoration: none;
                text-align: center;

                font-size: 24px;
                font-style: normal;
                font-weight: 400;
                line-height: 110%;
                font-family: var(--int);
                color: #000;

                @media (max-width: 1024px) {
                    font-size: 16px;
                    padding: 16px 0;
                    margin-bottom: 13px;
                }

                &:first-child {
                    background: #000;
                    color: #fff;
                }
            }
        }

        h1 {
            font-size: 32px;
            font-style: normal;
            font-weight: 500;
            line-height: normal;
            font-family: var(--int);
            color: #000;
            margin-bottom: 20px;

            @media (max-width: 1024px) {
                font-size: 24px;
            }
        }

    }
}

.custom-checkbox p,
.custom-checkbox a {
    @media (max-width: 1024px) {
        font-size: 12px !important;
    }
}

.custom-checkbox input[type="checkbox"] {
    opacity: 0;
    position: absolute;
    border-radius: 3px;
}

.custom-checkbox .checkbox-text:before {
    content: '';
    display: inline-block;
    vertical-align: middle;
    width: 30px;
    height: 30px;
    margin-right: 10px;
    border: 2px solid #000;
    border-radius: 0;
    margin-bottom: 3px;

    @media (max-width: 1024px) {
        width: 20px;
        height: 20px;
    }
}

.custom-checkbox input[type="checkbox"]:checked+.checkbox-text:before {
    content: url('@/assets/img/check.svg');
    font-size: 30px;
    color: black;
    text-align: center;
    line-height: 20px;
    background: transparent;
}

.custom-checkbox {
    margin-bottom: 20px;

}

.custom-checkbox:last-child {
    margin-bottom: 0 !important;

    @media (max-width: 1024px) {
        margin-bottom: 22px !important;
    }
}
</style>