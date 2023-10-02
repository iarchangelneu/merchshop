<template>
    <header v-if="!hideHeaderOnPages.includes($route.name)">
        <div class="header__block">
            <div class="headerbody">
                <div class="dnone"></div>
                <NuxtLink to="/"> <img style="margin-left: 120px" class="logo" src="@/assets/img/headerlogo.svg" alt="">
                </NuxtLink>


                <div class="right">
                    <img src="@/assets/img/cart.svg" v-if="accountUrl == '/buyer-account'" style="cursor: pointer;" alt=""
                        @click.stop="toggleCart">
                    <NuxtLink :to="accountUrl">
                        <img src="@/assets/img/account.svg" alt="">
                    </NuxtLink>
                    <NuxtLink to="/withdrawal" v-if="accountUrl == '/buyer-account' || accountUrl == '/seller-account'">
                        <img src="@/assets/img/cash.svg" class="cash" alt="">
                    </NuxtLink>

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
                        <a href="/catalog">Каталог</a>
                        <NuxtLink to="/about">о нас</NuxtLink>
                        <NuxtLink to="/withdrawal" class="refill">Кошелек <img src="@/assets/img/cash.svg" alt="">
                        </NuxtLink>
                        <small v-if="userBalance !== null">{{ userBalance == null ? '0 ₸' : userBalance.toLocaleString()
                            + ' ₸' }} </small>
                    </div>

                    <NuxtLink to="/login" class="login"
                        v-if="accountUrl !== '/seller-account' && accountUrl !== '/buyer-account'">Войти / регистрация
                    </NuxtLink>

                    <div class="links moblinks">
                        <a href="/catalog/?category=1" :class="{ 'link--active': $route.query.category === '1' }">
                            Стикеры</a>
                        <a href="/catalog/?category=2" :class="{ 'link--active': $route.query.category === '2' }">
                            Одежда
                        </a>
                        <a href="/catalog/?category=3" :class="{ 'link--active': $route.query.category === '3' }">Чехлы
                            на
                            телефон</a>
                        <a href="/catalog/?category=4" :class="{ 'link--active': $route.query.category === '4' }">
                            Постеры</a>
                        <a href="/catalog/?category=5" :class="{ 'link--active': $route.query.category === '5' }">Для
                            дома</a>
                        <a href="/catalog/?category=6" :class="{ 'link--active': $route.query.category === '6' }">
                            Аксессуары</a>
                        <a href="/catalog/?category=7" :class="{ 'link--active': $route.query.category === '7' }">Для
                            питомцев</a>
                        <a href="/catalog/?category=8" :class="{ 'link--active': $route.query.category === '8' }">
                            Канцелярия</a>
                        <a href="/catalog/?category=9" :class="{ 'link--active': $route.query.category === '9' }">Для
                            детей
                        </a>
                        <a href="/catalog/?category=10" :class="{ 'link--active': $route.query.category === '10' }">
                            Подарочные наборы</a>
                    </div>
                </div>

            </div>
            <div class="categories" :style="{
                '--categories-opacity': isCategoriesVisible ? '1' : '0',
                '--categories-pointer-events': isCategoriesVisible ? 'auto' : 'none',
            }" v-if="isCategoriesVisible">
                <a href="/catalog/?category=1" :class="{ 'link--active': $route.query.category === '1' }">
                    Стикеры</a>
                <a href="/catalog/?category=2" :class="{ 'link--active': $route.query.category === '2' }">
                    Одежда
                </a>
                <a href="/catalog/?category=3" :class="{ 'link--active': $route.query.category === '3' }">Чехлы
                    на
                    телефон</a>
                <a href="/catalog/?category=4" :class="{ 'link--active': $route.query.category === '4' }">
                    Постеры</a>
                <a href="/catalog/?category=5" :class="{ 'link--active': $route.query.category === '5' }">Для
                    дома</a>
                <a href="/catalog/?category=6" :class="{ 'link--active': $route.query.category === '6' }">
                    Аксессуары</a>
                <a href="/catalog/?category=7" :class="{ 'link--active': $route.query.category === '7' }">Для
                    питомцев</a>
                <a href="/catalog/?category=8" :class="{ 'link--active': $route.query.category === '8' }">
                    Канцелярия</a>
                <a href="/catalog/?category=9" :class="{ 'link--active': $route.query.category === '9' }">Для
                    детей
                </a>
                <a href="/catalog/?category=10" :class="{ 'link--active': $route.query.category === '10' }">
                    Подарочные наборы</a>
            </div>
        </div>

        <div class="cart" :class="{ cartOpen: cartOpen }" @click="stopPropagation">
            <div class="cart__header">
                <h1>корзина</h1>
                <img src="@/assets/img/closecart.svg" @click="closeCart" style="cursor: pointer;" alt="">
            </div>

            <div class="cart__body">
                <div class="cart__item" v-for="item in cart" :key="item.id">
                    <img :src="pathUrl + '/api' + item.products.add_image[0].image" class="main__cart" alt="">

                    <div>
                        <h2>{{ item.products.name }}</h2>

                        <div class="price">
                            <h2 v-if="item.products.discount > 0">{{ (Math.floor((item.products.price -
                                ((item.products.price
                                    * item.products.discount)
                                    /
                                    100))) * item.amount).toLocaleString() + ' ₸' }}</h2>
                            <h2 v-else>{{ item.products.price == 0 ? 'Бесплатно' : (item.products.price *
                                item.amount).toLocaleString() + ' ₸' }}
                            </h2>
                            <div class="counter">
                                <img src="@/assets/img/minus.svg" alt="" @click="decrement(item)">
                                <span>{{ item.amount }}</span>
                                <img src="@/assets/img/plus.svg" @click="increment(item)" alt="">
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
import global from '~/mixins/global';
import axios from 'axios';
export default {
    mixins: [global],
    data() {
        return {
            menuOpen: false,
            isCategoriesVisible: true,
            lastScrollTop: 0,
            cartOpen: false,
            hideHeaderOnPages: ['login', 'register'],
            pathUrl: 'https://merchshop.kz',
            userBalance: null,
            accountType: '',
            accountUrl: 'false',
            cart: [],
        }
    },
    mounted() {
        window.addEventListener("scroll", this.handleScroll);
        const accType = localStorage.getItem('accountType')
        if (accType == 'buyer-account') {
            this.getBuyer()
            this.getCart()
            this.accountType = 'buyer'
            setInterval(() => {
                this.cartLength = localStorage.getItem('cartLength')
            }, 1);
        }
        else if (accType == 'seller-account') {
            this.getSeller()
            this.accountType = 'seller'
        }
        else {
            console.log('not authorized')
        }
    },
    methods: {
        increment(item) {
            item.amount++;
            console.log(item)
            this.changeAmount(item)
        },
        decrement(item) {
            if (item.amount > 0) {
                item.amount--;
                console.log(item)
                this.changeAmount(item)
            }
            if (item.amount <= 0) {
                item.amount = 1
                this.deleteFromCart(item.id)
            }
        },
        toggleCart() {
            this.cartOpen = !this.cartOpen;
            if (this.cartOpen) {
                document.addEventListener('click', this.closeCart);
                this.getCart()
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
        changeAmount(item) {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/buyer/all-product-basket`;
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;

            axios
                .put(path, item)
                .then((res) => {
                    console.log(res)
                    //     this.getCart()
                })
                .catch((error) => {
                    console.error(error);

                });
        },
        getCart() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/buyer/all-product-basket`;
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;

            axios
                .get(path)
                .then(response => {
                    this.cart = response.data
                })
                .catch(error => {
                    console.error(error)
                })
        },
        deleteFromCart(id) {
            const token = this.getAuthorizationCookie()
            const csrf = this.getCSRFToken()
            const path = `${this.pathUrl}/api/buyer/delete-product-basket/${id}`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            axios
                .put(path)
                .then(response => {
                    console.log(response)
                    this.getCart()
                })
                .catch(error => {
                    console.error(error)
                })
        },
        getBuyer() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/buyer/buyer-lk`;
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios
                .get(path)
                .then(response => {
                    this.userBalance = response.data.balance

                })
                .catch(error => console.log(error));
        },
        getSeller() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/seller/seller-lk`;
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios
                .get(path)
                .then(response => {
                    this.userBalance = response.data.balance

                })
                .catch(error => console.log(error));
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

    .refill {
        display: none;

        @media(max-width: 1024px) {
            display: flex;
            align-items: center;
            gap: 10px;
        }
    }

    .dnone {
        @media (max-width: 1024px) {
            display: none;
        }
    }

    .cash {
        @media (max-width: 1024px) {
            display: none;
        }
    }

    .logo {
        @media (max-width: 1024px) {
            margin: 0 !important;
        }
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

        @media (max-width: 1600px) {
            width: 45%;
        }

        @media (max-width: 1024px) {
            width: 100%;
            padding: 20px;
            border: 0 !important;
        }

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
                align-items: flex-start;
                gap: 20px;
                margin-bottom: 30px;

                .main__cart {
                    width: 185px;
                    height: 167px;
                    object-fit: cover;

                    @media (max-width: 1024px) {
                        width: 95px;
                        height: 95px;
                    }
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

                        @media (max-width: 1024px) {
                            font-size: 16px;
                        }
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

            @media (max-width: 1024px) {
                margin-bottom: 20px;
            }

            h1 {
                font-size: 32px;
                font-style: normal;
                font-weight: 500;
                line-height: normal;
                text-transform: uppercase;
                font-family: var(--int);
                color: #000;
                margin: 0;

                @media (max-width: 1024px) {
                    font-size: 20px;
                }
            }
        }
    }

    .header__block {
        position: fixed;
        width: 100%;
        padding: 21px 100px;
        z-index: 100;
        background: #FFFFF3;

        @media (max-width: 1600px) {
            padding: 21px 50px;
        }

        @media (max-width: 1024px) {
            padding: 21px 20px;
        }
    }

    .categories {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 40px;
        margin-top: 25px;

        @media (max-width: 1430px) {
            display: none;
        }

        transition: all .3s ease;

        a {
            font-size: 18px;
            font-style: normal;
            font-weight: 400;
            line-height: normal;
            text-transform: uppercase;
            font-family: var(--int);
            color: #000;

            @media (max-width: 1600px) {
                font-size: 14px;
            }
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

        @media (max-width: 1024px) {
            width: 100%;
        }

        .moblinks {
            display: none !important;
            margin-top: 20px;

            @media (max-width: 1430px) {
                display: flex !important;
            }

            a {
                font-weight: 400 !important;
            }
        }

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

        small {
            font-family: var(--nt);
            color: #000;
            font-size: 20px;
            font-weight: 500;
        }

        .login {
            margin: 74px 0 0 !important;
            display: inline-block;

            @media (max-width: 1430px) {
                margin: 20px 0 0 !important;
            }
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