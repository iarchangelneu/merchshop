<template>
    <header>
        <div class="dnone"></div>
        <img src="@/assets/img/headerlogo.svg" alt="">

        <div class="right">
            <img src="@/assets/img/cart.svg" alt="">
            <img src="@/assets/img/account.svg" alt="">
            <img src="@/assets/img/cash.svg" alt="">

            <div class="burg">
                <input id="menu__toggle" class="d-none" type="checkbox" />
                <label class="menu__btn" for="menu__toggle" @click="menuOpen = !menuOpen">
                    <span></span>
                </label>
            </div>
        </div>
        <div class="headermenu" :class="{ opened: menuOpen }">

            <div class="links">
                <NuxtLink to="/#sales">Акции и скидки</NuxtLink>
                <NuxtLink to="/catalog">Каталог</NuxtLink>
                <NuxtLink to="/about">о нас</NuxtLink>
            </div>

            <NuxtLink to="/login" class="login">Войти / регистрация</NuxtLink>
        </div>
    </header>
</template>
<script>
export default {
    data() {
        return {
            menuOpen: false,
        }
    }
}
</script>
<style lang="scss" scoped>
header {
    position: relative;
    display: flex;
    justify-content: space-between;
    align-items: center;

    position: fixed;
    width: 100%;
    padding: 21px 100px;
    z-index: 100;
    background: #FFFFF3;

    .opened {
        transform: rotate3d(1, 1, 1, 0) !important;
    }

    .headermenu {
        position: absolute;
        top: 100%;
        right: 5%;
        transform: rotate3d(1, 1, 1, -240deg);
        perspective: 400px;
        transition: all .5s ease;

        border: 2px solid #D2D2D2;
        background: #fff;
        padding: 30px;

        .links {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        a {
            font-size: 20px;
            font-style: normal;
            font-weight: 500;
            line-height: normal;
            text-transform: uppercase;
            font-family: var(--int);
            color: #000;
        }

        .login {
            margin: 74px 0 0 !important;
            display: inline-block;
        }
    }

    .right {
        display: flex;
        gap: 20px;

        #menu__toggle {
            opacity: 0;
        }

        .menu__btn {
            margin-top: 10px;
            display: flex;
            /* используем flex для центрирования содержимого */
            align-items: center;
            /* центрируем содержимое кнопки */
            width: 35px;
            height: 20px;
            cursor: pointer;
            z-index: 100000000;
            color: #fff;
            position: relative;
            transform: rotate(180deg);
        }

        .menu__btn>span {
            display: block;
            position: absolute;
            width: 100%;
            height: 2px;
            background-color: #000;
        }

        .menu__btn>span::before,
        .menu__btn>span::after {
            display: block;
            position: absolute;
            width: 100%;
            height: 2px;
            background-color: #000;
        }

        .menu__btn>span::before {
            content: '';
            top: -8px;
        }

        .menu__btn>span::after {
            content: '';
            top: 8px;
        }

        #menu__toggle:checked~.menu__btn>span {
            transform: rotate(45deg);
            background-color: #000;
            border-radius: 10px;

        }

        #menu__toggle:checked~.menu__btn>span::before {
            top: 0;
            transform: rotate(0);
            background-color: #000;
            border-radius: 10px;

        }

        #menu__toggle:checked~.menu__btn>span::after {
            top: 0;
            transform: rotate(90deg);
            background-color: #000;
            border-radius: 10px;
        }

        #menu__toggle:checked~.menu__box {
            visibility: visible;
            top: 0;
        }

        .menu__btn>span,
        .menu__btn>span::before,
        .menu__btn>span::after {
            transition-duration: .25s;
        }
    }
}
</style>