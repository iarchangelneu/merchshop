<template>
    <div class="money">

        <div class="money__body">
            <div class="text-center">
                <h1>Вывод средств</h1>
            </div>
            <div class="type" v-if="accountType == 'buyer'">
                <NuxtLink to="/refill">
                    Пополнение
                </NuxtLink>
                <NuxtLink to='/withdrawal'>
                    Вывод
                </NuxtLink>
            </div>

            <p>Порядок действий для вывода средств</p>
            <p>1. Подтвердите Ваше согласие с правилами нашей системы</p>

            <label class="custom-checkbox">
                <input type="checkbox">
                <p class="checkbox-text m-0">Я согласен с <NuxtLink to="/terms">пользовательским соглашением
                    </NuxtLink>
                    и <NuxtLink to="/polytics">политикой конфиденциальности</NuxtLink>
                </p>
            </label>

            <p>2. Введите сумму, которую вы хотите вывести с личного счета, и нажмите на кнопку «Вывести». Вы будете
                переадресованы на сайт платёжной системы, где сможете завершить операцию.</p>

            <div class="card">
                <input type="text" class="mb-3 w-100" name="card" id="card" v-model="cardNumber"
                    :maxlength="cardNumberMaxLength" placeholder="Введите номер карты" @input="formatCardNumber"
                    autocomplete="cc-number">
                <input type="text" class="mb-3 w-100" name="cardHolder" id="card" v-model="cardHolder"
                    placeholder="Введите владельца карты" autocomplete="cc-name">
            </div>

            <div class="input">
                <input type="number" name="count" id="count" placeholder="100 ₸" v-model="count">
                <button ref="outBtn" @click="outMoney()">Пополнить</button>
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
import global from '~/mixins/global';
import axios from 'axios';
export default {
    mixins: [global],
    data() {
        return {
            count: null,
            cardNumber: '',
            cardHolder: '',
            cardNumberMaxLength: 19,
            accountType: '',
            pathUrl: 'https://merchshop.kz',

        }
    },
    methods: {
        outMoney() {
            const token = this.getAuthorizationCookie()
            const csrf = this.getCSRFToken()
            const path = `${this.pathUrl}/api/money/pay-return`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            this.$refs.outBtn.innerHTML = 'Ожидайте'

            axios
                .post(path, {
                    amount: this.count,
                    card_number: this.cardNumber.replace(/\s/g, ''),
                    cardholder: this.cardHolder
                })
                .then(response => {
                    console.log(response)
                    if (response.status == 200) {
                        this.$refs.outBtn.innerHTML = 'Успешно'
                    }
                    if (response.status == 228) {
                        if (response.data.error_msg == 'ov_merchant_balance_insufficient') {
                            this.$refs.outBtn.innerHTML = 'Недостаточно средств'
                        }
                        else {
                            this.$refs.outBtn.innerHTML = response.data.error_msg
                        }

                    }

                })
                .catch(error => {
                    console.error(error)
                    this.$refs.outBtn.innerHTML = 'ВЫВЕСТИ'
                })
        },
        formatCardNumber() {
            this.cardNumber = this.cardNumber.replace(/\D/g, '');
            this.cardNumber = this.cardNumber.replace(/(.{4})/g, '$1 ');
            this.cardNumber = this.cardNumber.slice(0, this.cardNumberMaxLength);
        }
    },
    watch: {
        cardNumber(newCardNumber) {
            this.cardHolder = this.cardNumberToHolderMapping[newCardNumber] || "";
        }
    },
    mounted() {
        const accType = localStorage.getItem('accountType')
        if (accType !== 'buyer-account' && accType !== 'seller-account') {
            window.location.href = '/login'
        }
        if (accType == 'buyer-account') {
            this.accountType = 'buyer'

        }
        else if (accType == 'seller-account') {
            this.accountType = 'seller'
        }
        else {
            return
        }

    },
}
</script>
<script setup>
useSeoMeta({
    title: 'Вывод средств | MerchShop',
    ogTitle: 'Вывод средств | MerchShop',
    description: 'Вывод средств | MerchShop',
    ogDescription: 'Вывод средств | MerchShop',
})
</script>
<style lang="scss" scoped>
.money {
    padding: 150px 0 60px;
    display: flex;
    justify-content: center;
    align-items: center;
    //  height: 100vh;

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

        .card {
            background: 0;
            border: 0;

            input {
                background: transparent;
                border: 2px solid #000;
                padding: 12px 10px;
                border-radius: 0;

                font-size: 20px;
                font-family: var(--int);
                color: #000;
            }
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

        .type {
            display: flex;
            margin-bottom: 20px;

            @media (max-width: 1024px) {
                margin-bottom: 0;
            }

            a {
                flex: 1;
                padding: 12px;
                background: #000;
                border: 2px solid #000;
                text-decoration: none;
                text-align: center;

                font-size: 24px;
                font-style: normal;
                font-weight: 400;
                line-height: 110%;
                font-family: var(--int);
                color: #fff;

                @media (max-width: 1024px) {
                    font-size: 16px;
                    padding: 16px 0;
                    margin-bottom: 13px;
                }

                &:first-child {
                    background: #fff;
                    color: #000;
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