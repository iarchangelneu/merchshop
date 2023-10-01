<template>
    <div class="page">
        <div class="form__body">
            <div>
                <h1>Регистрация</h1>

                <input type="email" name="email" id="email" v-model="email" placeholder="Эл.почта" ref="email">
                <input type="password" name="password" id="password" v-model="password" placeholder="Пароль" ref="password">
                <input type="password" name="password" id="password" v-model="password__repeat"
                    placeholder="Повторите Пароль" ref="repeat__password">
                <input type="text" name="name" id="name" v-model="name" placeholder="Отображаемое имя" ref="name">
                <div class="type">
                    <button :class="{ activeBtn: userType == 'seller' }" @click="userType = 'seller'">
                        Продавец
                    </button>
                    <button :class="{ activeBtn: userType == 'buyer' }" @click="userType = 'buyer'">
                        Покупатель
                    </button>
                </div>
                <label class="custom-checkbox text-left">
                    <input type="checkbox" v-model="checked">
                    <p class="checkbox-text m-0" ref="checked">Я согласен с <NuxtLink to="/terms">пользовательским
                            соглашением
                        </NuxtLink>
                        и <NuxtLink to="/polytics">политикой конфиденциальности</NuxtLink>
                    </p>
                </label>

                <div class="text-center">
                    <small>{{ error }}</small>
                    <button @click="register()">зарегистрироваться</button>

                    <span>Уже есть аккаунт? <NuxtLink to='/login'>Вход</NuxtLink></span>
                </div>
            </div>
        </div>

        <div class="img">
            <img src="@/assets/img/logreg.png" class="img-fluid" alt="">
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
            email: '',
            password: '',
            password__repeat: '',
            name: '',
            checked: false,
            error: '',
            userType: 'seller',
            pathUrl: 'https://merchshop.kz',
        }
    },
    methods: {
        register() {
            const buyer = `${this.pathUrl}/api/main/registration/buyer`
            const seller = `${this.pathUrl}/api/main/registration/seller`
            const csrf = this.getCSRFToken()

            if (this.email !== '') {
                this.error = ''
                this.$refs.email.style.borderColor = '#fff'

                if (this.password != 0 && this.password == this.password__repeat) {
                    this.$refs.password.style.borderColor = '#fff'
                    this.$refs.repeat__password.style.borderColor = '#fff'
                    this.error = ''

                    if (this.checked) {
                        this.$refs.checked.style.color = '#fff'
                        if (this.name !== '') {
                            if (this.userType == 'seller') {

                                this.$refs.name.style.borderColor = '#fff'
                                this.error = ''
                                axios.defaults.headers.common['X-CSRFToken'] = csrf;
                                axios
                                    .post(seller, { first_name: this.name, password: this.password, username: this.email, email: this.email })
                                    .then((res) => {

                                        document.cookie = `Authorization=${res.data.token}; expires=Fri, 31 Dec 2023 23:59:59 GMT; path=/`;
                                        console.log(res)
                                        localStorage.setItem('accountType', res.data.redirect_url)
                                        window.location.href = res.data.redirect_url
                                    })
                                    .catch((error) => {
                                        this.error = error.response.data.detail
                                        console.log(error.response);
                                    });

                            }
                            else {
                                axios.defaults.headers.common['X-CSRFToken'] = csrf;
                                this.error = ''
                                axios
                                    .post(buyer, { first_name: this.name, email: this.email, password: this.password, username: this.email, email: this.email })
                                    .then((res) => {

                                        document.cookie = `Authorization=${res.data.token}; expires=Fri, 31 Dec 2023 23:59:59 GMT; path=/`;
                                        console.log(res)
                                        localStorage.setItem('accountType', res.data.redirect_url)
                                        window.location.href = '/'
                                    })
                                    .catch((error) => {
                                        console.log(error.responseS);
                                        this.error = error.response.data.detail
                                    });
                            }
                        }
                        else {
                            this.error = 'Вы не заполнили имя'
                            this.$refs.name.style.borderColor = 'red'
                        }
                    }
                    else {
                        this.$refs.checked.style.color = 'red'
                        this.error = 'Вы не согласились с условиями'
                    }
                }
                else {
                    this.error = 'Пароли не совпадают'
                    this.$refs.password.style.borderColor = 'red'
                    this.$refs.repeat__password.style.borderColor = 'red'
                }
            }
            else {
                this.error = 'Вы не указали почту'
                this.$refs.email.style.borderColor = 'red'
            }
        }
    },
    mounted() {
        const accType = localStorage.getItem('accountType')
        if (accType == 'buyer-account') {
            window.location.href = '/buyer-account'
        }
        else if (accType == 'seller-account') {
            window.location.href = '/seller-account'
        }
        else {
            console.log('not authorized')
        }

    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Регистрация | MerchShop',
    ogTitle: 'Регистрация | MerchShop',
    description: 'Регистрация | MerchShop',
    ogDescription: 'Регистрация | MerchShop',
})
</script>
<style lang="scss" scoped>
.page {
    display: flex;
    align-items: center;

    small {
        margin-bottom: 20px;
        text-align: left !important;
        display: block;
        color: red;
        font-family: var(--int);
        font-size: 14px;
    }

    @media (max-width: 1024px) {
        flex-direction: column;
        padding: 0 20px;
    }

    .type {
        display: flex;
        gap: 27px;

        .activeBtn {
            background: #fff !important;
            color: #000 !important;
        }

        button {
            flex: 1;
            transition: all .3s ease;
        }
    }

    .img {
        display: flex;
        align-items: center;
        justify-content: center;
        height: 100vh;
        width: 100%;

        @media (max-width: 1024px) {
            height: auto;
            margin-top: 40px;
        }
    }


    .form__body {
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
        max-width: 647px;
        padding: 0 100px;

        //   // background: url('@/assets/img/logtex.svg'), lightgray 0% 0% / 40.00000059604645px 40.00000059604645px repeat;
        background-color: #F7BFCA;

        @media (max-width: 1024px) {
            height: auto;
            margin-top: 100px;
            padding: 40px 25px;
            max-width: 100%;
        }

        p,
        a {
            font-size: 16px;
            font-style: normal;
            font-weight: 400;
            line-height: 130%;
            font-family: var(--int);
            color: #fff;
            margin-bottom: 20px !important;

            a {
                color: #fff;
                text-decoration: underline;
            }

            @media (max-width: 1024px) {
                font-size: 12px;
            }
        }

        div {
            width: 100%;
            text-align: center;
        }

        span {
            display: block;
            font-size: 16px;
            font-style: normal;
            font-weight: 400;
            line-height: 110%;
            font-family: var(--int);
            color: #fff;

            a {
                color: #fff;
                text-decoration: underline;
            }
        }

        button {
            padding: 10px 13px;
            background: transparent;
            border: 2px solid #fff;

            font-size: 16px;
            font-style: normal;
            font-weight: 500;
            line-height: normal;
            text-transform: uppercase;
            font-family: var(--int);
            color: #fff;
            margin-bottom: 20px;
        }

        input {
            display: block;
            width: 100%;
            margin-bottom: 30px;

            background: #fff;
            border: 2px solid #fff;
            padding: 10px 15px;

            font-size: 16px;
            font-style: normal;
            font-weight: 400;
            line-height: 130%;
            font-family: var(--int);
            color: #000;

            @media (max-width: 1024px) {
                height: 40px;
            }
        }

        h1 {
            font-size: 64px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            font-family: var(--int);
            color: #fff;
            margin: 0 0 30px;

            @media (max-width: 1024px) {
                font-size: 40px;
            }
        }
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
    width: 20px;
    height: 20px;
    margin-right: 10px;
    border: 2px solid #fff;
    border-radius: 0;
    margin-bottom: 3px;
}

.custom-checkbox input[type="checkbox"]:checked+.checkbox-text:before {
    content: url('@/assets/img/check.svg');
    font-size: 10px;
    color: black;
    text-align: center;
    line-height: 10px;
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