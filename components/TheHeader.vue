<template>
    <header v-if="!hideHeaderOnPages.includes($route.name)">
        <div class="header__block">
            <div class="headerbody">
                <div class="dnone"></div>
                <NuxtLink to="/"> <img style="margin-left: 120px" src="@/assets/img/headerlogo.svg" alt=""></NuxtLink>


                <div class="right">
                    <img src="@/assets/img/cart.svg" style="cursor: pointer;" alt="" @click.stop="toggleCart">
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
                <NuxtLink to="/catalog/?category=stickers"
                    :class="{ 'link--active': $route.query.category === 'stickers' }">
                    Стикеры</NuxtLink>
                <NuxtLink to="/catalog/?category=cloth" :class="{ 'link--active': $route.query.category === 'cloth' }">
                    Одежда
                </NuxtLink>
                <NuxtLink to="/catalog/?category=cases" :class="{ 'link--active': $route.query.category === 'cases' }">Чехлы
                    на
                    телефон</NuxtLink>
                <NuxtLink to="/catalog/?category=posters" :class="{ 'link--active': $route.query.category === 'posters' }">
                    Постеры</NuxtLink>
                <NuxtLink to="/catalog/?category=households"
                    :class="{ 'link--active': $route.query.category === 'households' }">Для дома</NuxtLink>
                <NuxtLink to="/catalog/?category=accessories"
                    :class="{ 'link--active': $route.query.category === 'accessories' }">Аксессуары</NuxtLink>
                <NuxtLink to="/catalog/?category=pets" :class="{ 'link--active': $route.query.category === 'pets' }">Для
                    питомцев</NuxtLink>
                <NuxtLink to="/catalog/?category=office" :class="{ 'link--active': $route.query.category === 'office' }">
                    Канцелярия</NuxtLink>
                <NuxtLink to="/catalog/?category=kids" :class="{ 'link--active': $route.query.category === 'kids' }">Для
                    детей
                </NuxtLink>
                <NuxtLink to="/catalog/?category=gifts" :class="{ 'link--active': $route.query.category === 'gifts' }">
                    Подарочные наборы</NuxtLink>
            </div>
        </div>

        <div class="cart" :class="{ cartOpen: cartOpen }" @click="stopPropagation">
            <div class="cart__header">
                <h1>корзина</h1>
                <img src="@/assets/img/closecart.svg" @click="closeCart" style="cursor: pointer;" alt="">
            </div>

            <div class="cart__body">
                <div class="cart__item">
                    <img src="@/assets/img/cart.png" class="main__cart" alt="">

                    <div>
                        <h2>чехол на телефон</h2>

                        <div class="price">
                            <h2>4990 ₸</h2>
                            <div class="counter">
                                <img src="@/assets/img/minus.svg" alt="">
                                <span>1</span>
                                <img src="@/assets/img/plus.svg" alt="">
                            </div>
                        </div>
                    </div>
                </div>
                <div class="cart__item">
                    <img src="@/assets/img/cart.png" class="main__cart" alt="">

                    <div>
                        <h2>чехол на телефон</h2>

                        <div class="price">
                            <h2>4990 ₸</h2>
                            <div class="counter">
                                <img src="@/assets/img/minus.svg" alt="">
                                <span>1</span>
                                <img src="@/assets/img/plus.svg" alt="">
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="cart__footer">
                <NuxtLink to="/cart">перейти в корзину</NuxtLink>
            </div>
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
            cartOpen: false,
            hideHeaderOnPages: ['login', 'register'],
        }
    },
    mounted() {
        window.addEventListener("scroll", this.handleScroll);
    },
    methods: {
        toggleCart() {
            this.cartOpen = !this.cartOpen;
            if (this.cartOpen) {
                document.addEventListener('click', this.closeCart);
            } else {
                document.removeEventListener('click', this.closeCart);
            }
        },
        closeCart() {
            this.cartOpen = false;
            document.removeEventListener('click', this.closeCart);
        },
        stopPropagation(event) {
            event.stopPropagation();
        },
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
.link--active {
    text-decoration: underline !important;
}

header {
    position: fixed;
    z-index: 105;

    .cartOpen {
        transform: rotate3d(1, 0, 0, 0deg) !important;
    }

    .cart {
        position: fixed;
        right: 0;
        top: 95px;
        width: 33%;
        height: 100vh;
        z-index: 101;
        transition: all .3s ease;
        transform: rotate3d(1, 0, 0, 90deg);

        padding: 30px;
        background: #fff;
        border-top: 2px solid #D2D2D2;
        border-bottom: 2px solid #D2D2D2;
        border-left: 2px solid #D2D2D2;

        .cart__footer {
            a {
                padding: 10px 20px;
                background: transparent;
                border: 1px solid #D2D2D2;

                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: normal;
                text-transform: uppercase;
                font-family: var(--int);
                color: #000;
                text-decoration: none;
            }
        }

        .cart__body {

            .cart__item {
                display: flex;
                align-items: start;
                gap: 20px;
                margin-bottom: 30px;

                .main__cart {
                    width: 185px;
                    height: 167px;
                    object-fit: cover;
                }

                div {

                    h2,
                    span {
                        font-size: 20px;
                        font-style: normal;
                        font-weight: 500;
                        line-height: normal;
                        text-transform: uppercase;
                        font-family: var(--int);
                        color: #000;
                        margin: 0;
                    }

                    .price {
                        margin-top: 20px;
                        display: flex;
                        gap: 30px;

                        .counter {
                            display: flex;
                            align-items: center;
                            gap: 20px;



                            img {
                                cursor: pointer;
                            }
                        }
                    }
                }
            }
        }

        .cart__header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;

            h1 {
                font-size: 32px;
                font-style: normal;
                font-weight: 500;
                line-height: normal;
                text-transform: uppercase;
                font-family: var(--int);
                color: #000;
                margin: 0;
            }
        }
    }

    .header__block {
        position: fixed;
        width: 100%;
        padding: 21px 100px;
        z-index: 100;
        background: #FFFFF3;
    }

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