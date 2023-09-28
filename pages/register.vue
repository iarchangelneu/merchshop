<template>
    <div class="page">
        <div class="form__body">
            <div>
                <h1>Регистрация</h1>

                <input type="email" name="email" id="email" v-model="email" placeholder="Эл.почта">
                <input type="password" name="password" id="password" v-model="password" placeholder="Пароль">
                <input type="password" name="password" id="password" v-model="password__repeat"
                    placeholder="Повторите Пароль">
                <input type="text" name="name" id="name" v-model="name" placeholder="Отображаемое имя">

                <label class="custom-checkbox text-left">
                    <input type="checkbox">
                    <p class="checkbox-text m-0">Я согласен с <NuxtLink to="/terms">пользовательским соглашением
                        </NuxtLink>
                        и <NuxtLink to="/polytics">политикой конфиденциальности</NuxtLink>
                    </p>
                </label>

                <div class="text-center">
                    <button>зарегистрироваться</button>

                    <span>Уже есть аккаунт? <NuxtLink to='/register'>Вход</NuxtLink></span>
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
            password__repeat: '',
            name: '',
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