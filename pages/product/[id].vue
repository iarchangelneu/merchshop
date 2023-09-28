<template>
    <div class="product">
        <PrevPage></PrevPage>

        <div class="product__block">
            <h1>чехол на телефон</h1>

            <div class="product__body">
                <div class="product__images">
                    <div class="main__image">
                        <img src="@/assets/img/product1.png" alt="">
                    </div>
                    <div class="slider__block">

                        <div class="image__slider">
                            <img src="@/assets/img/product2.png" alt="">
                            <img src="@/assets/img/product2.png" alt="">
                            <img src="@/assets/img/product2.png" alt="">
                            <img src="@/assets/img/product2.png" alt="">
                        </div>

                    </div>
                </div>
                <div class="product__desc">
                    <h2>Силиконовый чехол для телефона Iphone 13</h2>
                    <div v-html="description"></div>

                    <div class="add__infgo">
                        <span class="seller">Продавец: <NuxtLink to='/'>ShopCases</NuxtLink></span>
                        <span>Материал: <small>силикон</small></span>
                        <span>Производитель: <small>Китай</small></span>

                        <div class="price">
                            <h3>4990 ₸</h3>
                            <button>добавить в корзину</button>
                        </div>
                    </div>
                </div>
                <div class="product__author">
                    <span>Продавец: <NuxtLink to='/'>ShopCases</NuxtLink></span>
                </div>
            </div>

            <div class="similar__products">
                <h1>похожие товары</h1>

                <div class="similar__body">
                    <NuxtLink to="/catalog" class="similar__block">
                        <img src="@/assets/img/sale3.png" alt="">

                        <h1>ЧЕХОЛ С POP SOCKET</h1>

                        <div class="price">
                            <div>
                                <span>6990 ₸</span>
                                <small>7690 ₸</small>
                            </div>

                            <p class="mb-0">-10%</p>
                        </div>
                    </NuxtLink>
                    <NuxtLink to="/catalog" class="similar__block">
                        <img src="@/assets/img/sale3.png" alt="">

                        <h1>ЧЕХОЛ С POP SOCKET</h1>

                        <div class="price">
                            <div>
                                <span>6990 ₸</span>
                                <small>7690 ₸</small>
                            </div>

                            <p class="mb-0">-10%</p>
                        </div>
                    </NuxtLink>
                    <NuxtLink to="/catalog" class="similar__block">
                        <img src="@/assets/img/sale3.png" alt="">

                        <h1>ЧЕХОЛ С POP SOCKET</h1>

                        <div class="price">
                            <div>
                                <span>6990 ₸</span>
                                <small>7690 ₸</small>
                            </div>

                            <p class="mb-0">-10%</p>
                        </div>
                    </NuxtLink>
                    <NuxtLink to="/catalog" class="similar__block">
                        <img src="@/assets/img/sale3.png" alt="">

                        <h1>ЧЕХОЛ С POP SOCKET</h1>

                        <div class="price">
                            <div>
                                <span>6990 ₸</span>
                                <small>7690 ₸</small>
                            </div>

                            <p class="mb-0">-10%</p>
                        </div>
                    </NuxtLink>
                    <NuxtLink to="/catalog" class="similar__block">
                        <img src="@/assets/img/sale3.png" alt="">

                        <h1>ЧЕХОЛ С POP SOCKET</h1>

                        <div class="price">
                            <div>
                                <span>6990 ₸</span>
                                <small>7690 ₸</small>
                            </div>

                            <p class="mb-0">-10%</p>
                        </div>
                    </NuxtLink>
                    <NuxtLink to="/catalog" class="similar__block">
                        <img src="@/assets/img/sale3.png" alt="">

                        <h1>ЧЕХОЛ С POP SOCKET</h1>

                        <div class="price">
                            <div>
                                <span>6990 ₸</span>
                                <small>7690 ₸</small>
                            </div>

                            <p class="mb-0">-10%</p>
                        </div>
                    </NuxtLink>
                </div>

                <div class="text-right showmore">
                    <button ref="showmore">показать еще</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import { Navigation } from 'swiper/modules';
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';
export default {
    data() {
        return {
            description: 'Описание тут будет Описание тут будет Описание тут будет Описание тут будет Описание тут будет Описание тут будет Описание тут будет Описание тут будет Описание тут будет Описание тут будет Описание тут будет',
            modules: [Navigation],
            navigation: {
                nextEl: '.next',
                prevEl: '.prev',
            },

            breakpoints: {
                320: {
                    slidesPerView: 1,
                    spaceBetween: 10,

                },
                1300: {
                    slidesPerView: 4,
                    spaceBetween: 25,
                }
            },
        }
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Страница товара | MerchShop',
    ogTitle: 'Страница товара | MerchShop',
    description: 'Страница товара | MerchShop',
    ogDescription: 'Страница товара | MerchShop',
})
</script>
<style lang="scss" scoped>
.product {
    padding: 150px 100px 60px;

    @media (max-width: 1600px) {
        padding: 150px 50px 60px;
    }

    @media (max-width: 1024px) {
        padding: 100px 20px 60px;
    }

    .similar__products {
        margin-top: 50px;

        @media (max-width: 1024px) {
            margin-top: 30px;
        }

        .showmore {
            margin-top: 30px;

            button {
                padding: 10px 20px;
                border: 1px solid #D2D2D2;
                background: transparent;

                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: normal;
                text-transform: uppercase;
                font-family: var(--int);
                color: #000;
            }
        }

        .similar__body {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(257px, 1fr));
            gap: 35px;
            grid-auto-flow: dense;

            @media (max-width: 1024px) {
                gap: 20px;
                grid-template-columns: repeat(auto-fill, minmax(165px, 1fr));
            }

            .similar__block {
                background: #fff;
                text-decoration: none;
                border: 1px solid #D2D2D2;
                padding: 10px;
                display: flex;
                flex-direction: column;
                max-width: 100%;

                @media (max-width: 1024px) {
                    max-width: 100%;
                }

                img {
                    width: 100%;
                    height: 214px;
                    object-fit: cover;

                    @media (max-width: 1024px) {
                        height: 130px;
                    }

                }

                h1 {
                    font-style: normal;
                    font-weight: 500;
                    line-height: normal;
                    text-transform: uppercase;
                    font-size: 20px;
                    font-family: var(--int);
                    color: #000;
                    margin-top: 10px;

                    @media (max-width: 1024px) {
                        font-size: 10px;
                    }
                }

                .price {
                    display: flex;
                    justify-content: space-between;
                    align-items: center;

                    div {
                        display: flex;
                        gap: 10px;

                        span {
                            font-size: 16px;
                            font-style: normal;
                            font-weight: 500;
                            line-height: normal;
                            text-transform: uppercase;
                            font-family: var(--int);
                            color: #000;

                            @media (max-width: 1024px) {
                                font-size: 12px;
                            }
                        }

                        small {
                            font-size: 12px;
                            font-style: normal;
                            font-weight: 500;
                            line-height: normal;
                            text-decoration-line: line-through;
                            text-transform: uppercase;
                            font-family: var(--int);
                            color: #828282;
                            margin-bottom: 4px;

                            @media (max-width: 1024px) {
                                font-size: 10px;
                            }
                        }
                    }

                    p {
                        font-size: 16px;
                        font-style: normal;
                        font-weight: 500;
                        line-height: normal;
                        text-transform: uppercase;
                        font-family: var(--int);
                        color: #828282;

                        @media (max-width: 1024px) {
                            font-size: 12px;
                        }
                    }
                }
            }
        }

        h1 {
            font-size: 20px;
            font-style: normal;
            font-weight: 600;
            line-height: normal;
            text-transform: uppercase;
            font-family: var(--int);
            color: #000;
        }
    }

    .product__block {

        .product__body {
            display: flex;
            gap: 60px;
            align-items: flex-start;

            @media (max-width: 1024px) {
                flex-direction: column;
                gap: 20px;
            }

            .product__author {
                @media (max-width: 1024px) {
                    display: none;
                }

                span {
                    font-size: 16px;
                    font-style: normal;
                    font-weight: 600;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;
                    white-space: nowrap;

                    a {
                        font-weight: 400;
                        text-decoration: underline;
                        color: #000;
                    }
                }

            }

            .product__desc {

                .add__infgo {
                    margin-top: 30px;

                    @media (max-width: 1024px) {
                        margin-top: 20px;
                    }

                    .seller {
                        display: none;

                        @media (max-width: 1024px) {
                            display: block;
                        }

                        a {
                            color: #000;
                            text-decoration: underline;
                            font-weight: 400;

                        }
                    }

                    .price {
                        margin-top: 10px;
                        display: flex;
                        gap: 30px;

                        @media (max-width: 1024px) {
                            flex-direction: column;
                            gap: 20px;
                            align-items: flex-start;
                        }

                        h3 {
                            font-size: 32px;
                            font-style: normal;
                            font-weight: 500;
                            line-height: normal;
                            text-transform: uppercase;
                            font-family: var(--int);
                            color: #000;
                            margin: 0;

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

                            @media (max-width: 1024px) {}
                        }
                    }

                    span {
                        display: block;
                        font-size: 16px;
                        font-style: normal;
                        font-weight: 600;
                        line-height: 130%;
                        font-family: var(--int);
                        color: #000;
                        margin-bottom: 20px;

                        small {
                            font-weight: 400;
                        }

                    }
                }

                h2 {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: normal;
                    text-transform: uppercase;
                    font-family: var(--int);
                    color: #000;
                    margin-bottom: 20px;

                    @media (max-width: 1024px) {
                        font-size: 16px;
                    }
                }

                div {
                    font-family: var(--int);
                    font-size: 16px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    max-width: 727px;
                }
            }

            .product__images {

                @media (max-width: 1024px) {
                    width: 100%;
                }

                .slider__block {

                    .image__slider {
                        margin-top: 25px;
                        display: grid;
                        grid-template-columns: repeat(auto-fill, minmax(125px, 1fr));
                        gap: 35px;
                        grid-auto-flow: dense;
                        padding: 0 15px;

                        @media (max-width: 1024px) {
                            gap: 23px;
                            grid-template-columns: repeat(auto-fill, minmax(70px, 1fr));
                            padding: 0;
                        }

                        img {
                            width: 100%;
                            height: 125px;
                            object-fit: cover;

                            @media (max-width: 1024px) {
                                height: 70px;
                            }
                        }
                    }


                }

                .main__image {
                    img {
                        width: 33.229vw;
                        height: 29.948vw;

                        @media (max-width: 1024px) {
                            width: 100%;
                            height: 300px;
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
            margin: 20px 0 30px;

            @media (max-width: 1024px) {
                font-size: 20px;
            }
        }
    }
}
</style>