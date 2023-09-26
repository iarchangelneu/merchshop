<template>
    <div class="cart">
        <PrevPage></PrevPage>
        <h1>Корзина</h1>

        <div class="cart__body">
            <div class="cart__items">
                <div class="cart__item">
                    <img src="@/assets/img/cart2.png" alt="" class="main__img">

                    <div>
                        <div class="name">
                            <h1>чехол на телефон</h1>
                            <img src="@/assets/img/deletecart.svg" alt="">
                        </div>
                        <div class="price">
                            <h1>4990 ₸</h1>
                            <div class="counter">
                                <img src="@/assets/img/minus.svg" alt="">
                                <span>1</span>
                                <img src="@/assets/img/plus.svg" alt="">
                            </div>
                        </div>
                    </div>
                </div>
                <div class="cart__item">
                    <img src="@/assets/img/cart2.png" alt="" class="main__img">

                    <div>
                        <div class="name">
                            <h1>чехол на телефон</h1>
                            <img src="@/assets/img/deletecart.svg" alt="">
                        </div>
                        <div class="price">
                            <h1>4990 ₸</h1>
                            <div class="counter">
                                <img src="@/assets/img/minus.svg" alt="">
                                <span>1</span>
                                <img src="@/assets/img/plus.svg" alt="">
                            </div>
                        </div>
                    </div>
                </div>
                <div class="cart__item">
                    <img src="@/assets/img/cart2.png" alt="" class="main__img">

                    <div>
                        <div class="name">
                            <h1>чехол на телефон</h1>
                            <img src="@/assets/img/deletecart.svg" alt="">
                        </div>
                        <div class="price">
                            <h1>4990 ₸</h1>
                            <div class="counter">
                                <img src="@/assets/img/minus.svg" alt="">
                                <span>1</span>
                                <img src="@/assets/img/plus.svg" alt="">
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="cart__complete">

                <div class="text-center">
                    <h1>Подтверждение покупки</h1>
                </div>

                <span>Товаров: 3</span>
                <span>итоговая сумма: 19 070 ₸</span>
                <small>Сумма будет списана с вашего счета</small>

                <div class="text-center">
                    <button>ПРОДОЛЖИТЬ ОФОРМЛЕНИЕ</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {

        }
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

    .cart__body {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        gap: 8.333vw;

        .cart__complete {
            border: 2px solid #D2D2D2;
            background: #fff;
            padding: 30px;
            width: 100%;
            max-width: 530px;

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
                        }

                        .counter {
                            display: flex;
                            align-items: center;
                            gap: 15px;



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