<template>
    <div class="cart">
        <PrevPage></PrevPage>
        <h1>Корзина</h1>

        <div class="cart__body">
            <div class="cart__items">
                <div class="cart__item" v-for="item in cart" :key="item.id">
                    <img :src="pathUrl + '/api' + item.products.add_image[0].image" alt="" class="main__img">

                    <div>
                        <div class="name">
                            <h2>{{ item.products.name }}</h2>
                            <img src="@/assets/img/deletecart.svg" @click="deleteFromCart(item.id)" alt="">
                        </div>
                        <div class="price">
                            <h1 v-if="item.products.discount > 0">{{ (Math.floor((item.products.price -
                                ((item.products.price
                                    * item.products.discount)
                                    /
                                    100))) * item.amount).toLocaleString() + ' ₸' }}</h1>
                            <h1 v-else>{{ item.products.price == 0 ? 'Бесплатно' : (item.products.price *
                                item.amount).toLocaleString() + ' ₸' }}
                            </h1>
                            <div class="counter">
                                <img src="@/assets/img/minus.svg" alt="" @click="decrement(item)">
                                <span>{{ item.amount }}</span>
                                <img src="@/assets/img/plus.svg" alt="" @click="increment(item)">
                            </div>
                        </div>
                        <!-- <h1>{{ item.products.price }}</h1> -->
                    </div>
                </div>
            </div>

            <div class="cart__complete">

                <div class="text-center">
                    <h1>Подтверждение покупки</h1>
                </div>

                <span>Товаров: {{ cart.length }}</span>
                <span>итоговая сумма: {{ formatPrice(calculateTotal()) }} ₸</span>
                <small>Сумма будет списана с вашего счета</small>

                <div class="text-center">
                    <button ref="buyBtn" @click="buyProduct()">ПРОДОЛЖИТЬ ОФОРМЛЕНИЕ</button>
                </div>
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
            cart: [],
            pathUrl: 'https://merchshop.kz',
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
        buyProduct() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/buyer/placed-basket`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            this.$refs.buyBtn.innerHTML = 'Оформляем'
            axios
                .get(path)
                .then(response => {
                    console.log(response)
                    if (response.status == 204) {
                        this.$refs.buyBtn.innerHTML = 'Недостаточно средств'
                    }
                    if (response.status == 201) {
                        // this.getBuyer()
                        this.$refs.buyBtn.innerHTML = 'Оплата прошла успешно'

                        setTimeout(() => {
                            window.location.href = `/completed/${response.data.id_order}`
                        }, 3);

                    }
                })
                .catch(error => {
                    console.error(error)
                })

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
        calculateTotal() {
            let total = 0;

            this.cart.forEach(item => {
                const { price, discount } = item.products;
                const discountedPrice = price * (1 - discount / 100);
                total += discountedPrice * item.amount;
            });

            return total;
        },
        formatPrice(price) {
            return price.toLocaleString('ru-RU');
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
    },
    mounted() {
        this.getCart()
    }
}
</script>
<script setup>

useSeoMeta({
    title: 'Корзина | MerchShop',
    ogTitle: 'Корзина | MerchShop',
    description: 'Корзина | MerchShop',
    ogDescription: 'Корзина | MerchShop',
})
</script>
<style lang="scss" scoped>
.cart {
    padding: 150px 100px 60px;

    @media (max-width: 1600px) {
        padding: 150px 50px 60px;
    }

    @media (max-width: 1024px) {
        padding: 100px 30px 60px 20px;
    }

    .cart__body {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        gap: 8.333vw;

        @media (max-width: 1024px) {
            flex-direction: column;
            gap: 30px;
        }

        .cart__complete {
            .text-center {
                text-align: left !important;
            }

            border: 2px solid #D2D2D2;
            background: #fff;
            padding: 30px;
            width: 100%;
            max-width: 530px;

            @media (max-width: 1024px) {
                border: 0;
                background: transparent;
                padding: 0;
            }

            span {
                display: block;

                &:first-of-type {
                    margin-bottom: 20px;
                }

                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: normal;
                text-transform: uppercase;
                font-family: var(--int);
                color: #000;
            }

            small {
                display: block;
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
                margin-top: 10px;

            }

            button {
                border: 1px solid #D2D2D2;
                background: transparent;
                padding: 10px 20px;

                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: normal;
                text-transform: uppercase;
                font-family: var(--int);
                color: #000;
                margin-top: 58px;

                @media (max-width: 1024px) {
                    margin-top: 20px;
                }
            }

            h1 {
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: normal;
                text-transform: uppercase;
                font-family: var(--int);
                color: #000;
                margin-bottom: 30px;
                margin-top: 0;

                @media (max-width: 1024px) {
                    font-size: 16px;
                    font-weight: 600;
                    margin-bottom: 20px;
                }
            }
        }

        .cart__items {
            width: 100%;

            .cart__item {
                width: 100%;
                display: flex;
                gap: 30px;
                align-items: flex-start;

                margin-bottom: 30px;

                @media (max-width: 1024px) {
                    gap: 15px;
                    margin-bottom: 20px;
                }

                &:last-child {
                    margin: 0;
                }

                div {
                    width: 100%;

                    .price {
                        display: flex;
                        gap: 60px;
                        width: 100%;
                        margin-top: 30px;

                        @media (max-width: 1024px) {
                            flex-direction: column;
                            gap: 23px;
                            margin-top: 10px;
                        }

                        h1,
                        span {
                            white-space: nowrap;
                            font-size: 32px;
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

                        .counter {
                            display: flex;
                            align-items: center;
                            gap: 15px;


                            span {
                                @media (max-width: 1024px) {
                                    font-size: 20px;
                                }
                            }

                            img {
                                cursor: pointer;

                                &:first-child {
                                    width: 13px;
                                    height: 29px;
                                }

                                &:last-child {
                                    width: 15px;
                                    height: 29px;
                                }
                            }
                        }
                    }

                    .name {
                        display: flex;
                        justify-content: space-between;
                        align-items: center;

                        h1 {
                            margin: 0;
                            font-size: 20px;
                            font-style: normal;
                            font-weight: 500;
                            line-height: normal;
                            text-transform: uppercase;
                            font-family: var(--int);
                            color: #000;

                            @media (max-width: 1024px) {
                                font-size: 16px;
                            }
                        }

                        img {
                            cursor: pointer;
                        }
                    }
                }

                .main__img {
                    width: 19.271vw;
                    height: 17.344vw;
                    object-fit: cover;

                    @media (max-width: 1024px) {
                        width: 95px;
                        height: 95px;
                    }
                }
            }
        }
    }

    h1 {
        font-size: 40px;
        font-style: normal;
        font-weight: 600;
        line-height: normal;
        text-transform: uppercase;
        font-family: var(--int);
        color: #000;
        margin: 10px 0 30px;
    }
}
</style>