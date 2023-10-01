<template>
    <div class="page">
        <div class="form__body">
            <div>
                <h1>Авторизация</h1>

                <input type="email" name="email" id="email" v-model="email" placeholder="Эл.почта">
                <input type="password" name="password" id="password" v-model="password" placeholder="Пароль">

                <div class="text-center">
                    <small>{{ error }}</small>
                    <button @click="login()">ВОЙТИ</button>

                    <span>Еще нет аккаунта? <NuxtLink to='/register'>Регистрация</NuxtLink></span>
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
            pathUrl: 'https://merchshop.kz',
            error: '',
        }
    },
    methods: {
        login() {
            const path = `${this.pathUrl}/api/main/authorization`
            const csrf = this.getCSRFToken()

            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            axios
                .post(path, { username: this.email, password: this.password })
                .then((res) => {



                    document.cookie = `Authorization=${res.data.token}; expires=Fri, 31 Dec 2023 23:59:59 GMT; path=/`;
                    localStorage.setItem('accountType', res.data.redirect_url)
                    if (res.data.redirect_url == 'buyer-account') {
                        window.location.href = '/'
                    }
                    if (res.data.redirect_url == 'seller-account') {
                        window.location.href = '/seller-account'
                    }


                    console.log(res)
                })
                .catch((error) => {
                    console.log(error);
                    this.error = error.response.data.non_field_errors.toString()
                });
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
    title: 'Авторизация | MerchShop',
    ogTitle: 'Авторизация | MerchShop',
    description: 'Авторизация | MerchShop',
    ogDescription: 'Авторизация | MerchShop',
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

    .img {
        display: flex;
        align-items: center;
        justify-content: center;
        height: 100vh;
        width: 100%;

        @media (max-width: 1024px) {
            height: auto;
            margin-top: 130px;
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

        //  // background: url('@/assets/img/logtex.svg'), lightgray 0% 0% / 40.00000059604645px 40.00000059604645px repeat;
        background-color: #F7BFCA;


        @media (max-width: 1024px) {
            height: auto;
            margin-top: 180px;
            padding: 40px 25px;
            max-width: 100%;
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
            padding: 10px 4.219vw;
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
</style>