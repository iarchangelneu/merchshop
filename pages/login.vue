<template>
    <div class="page">
        <div class="form__body">
            <div>
                <h1>Авторизация</h1>

                <input type="email" name="email" id="email" v-model="email" placeholder="Эл.почта">
                <input type="password" name="password" id="password" v-model="password" placeholder="Пароль">

                <div class="text-center">
                    <button>ВОЙТИ</button>

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
export default {
    data() {
        return {
            email: '',
            password: '',
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

    .img {
        display: flex;
        align-items: center;
        justify-content: center;
        height: 100vh;
        width: 100%;
    }


    .form__body {
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
        max-width: 647px;
        padding: 0 100px;

        background: url('@/assets/img/logtex.svg'), lightgray 0% 0% / 40.00000059604645px 40.00000059604645px repeat;
        background-color: #F7BFCA;


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
        }

        h1 {
            font-size: 64px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            font-family: var(--int);
            color: #fff;
            margin: 0 0 30px;
        }
    }
}
</style>