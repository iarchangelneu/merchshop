<template>
    <header>
        <div class="headerbody">
            <div class="dnone"></div>
            <NuxtLink to="/"> <img style="margin-left: 120px" src="@/assets/img/headerlogo.svg" alt=""></NuxtLink>


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
        </div>
        <div class="categories" :style="{
            '--categories-opacity': isCategoriesVisible ? '1' : '0',
            '--categories-pointer-events': isCategoriesVisible ? 'auto' : 'none',
        }" v-if="isCategoriesVisible">
            <NuxtLink to="/catalog">Стикеры</NuxtLink>
            <NuxtLink to="/catalog">Одежда</NuxtLink>
            <NuxtLink to="/catalog">Чехлы на телефон</NuxtLink>
            <NuxtLink to="/catalog">Постеры</NuxtLink>
            <NuxtLink to="/catalog">Для дома</NuxtLink>
            <NuxtLink to="/catalog">Аксессуары</NuxtLink>
            <NuxtLink to="/catalog">Для питомцев</NuxtLink>
            <NuxtLink to="/catalog">Канцелярия</NuxtLink>
            <NuxtLink to="/catalog">Для детей</NuxtLink>
            <NuxtLink to="/catalog">Подарочные наборы</NuxtLink>
        </div>
    </header>
</template>
<script>
export default {
    data() {
        return {
            menuOpen: false,
            isCategoriesVisible: true,
            lastScrollTop: 0,
        }
    },
    mounted() {
        window.addEventListener("scroll", this.handleScroll);
    },
    methods: {
        handleScroll() {
            const currentScrollTop = window.scrollY;

            if (currentScrollTop > this.lastScrollTop) {
                this.isCategoriesVisible = false;
            } else {
                this.isCategoriesVisible = true;
            }

            this.lastScrollTop = currentScrollTop;
        },
    },
    beforeDestroy() {
        window.removeEventListener("scroll", this.handleScroll);
    },
}
</script>
<style lang="scss" scoped>
header {
    position: fixed;
    width: 100%;
    padding: 21px 100px;
    z-index: 100;
    background: #FFFFF3;

    .categories {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 40px;
        margin-top: 25px;

        transition: all .3s ease;

        a {
            font-size: 18px;
            font-style: normal;
            font-weight: 400;
            line-height: normal;
            text-transform: uppercase;
            font-family: var(--int);
            color: #000;
        }

        opacity: var(--categories-opacity, 1);
        pointer-events: var(--categories-pointer-events, auto);
    }

    .headerbody {
        position: relative;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .opened {
        transform: rotate3d(1, 1, 1, 0) !important;
    }

    .headermenu {
        position: absolute;
        top: 100%;
        right: 0;
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