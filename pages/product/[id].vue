<template>
    <div class="product">
        <PrevPage></PrevPage>
        <div v-if="product.length <= 0"></div>
        <div class="product__block" v-else>
            <h1>{{ category }}</h1>

            <div class="product__body">
                <div class="product__images">
                    <div class="main__image">
                        <img :src="product.add_image[0].image" alt="">
                    </div>
                    <div class="slider__block">

                        <div class="image__slider">
                            <img v-for="item in filteredImages" :key="item.id" :src="item.image">
                        </div>

                    </div>
                </div>
                <div class="product__desc">
                    <h2>{{ product.name }}</h2>
                    <div v-html="product.description"></div>

                    <div class="add__infgo">
                        <span class="seller">Продавец: <NuxtLink :to='"/seller/" + seller.id'>{{ seller.user.first_name }}
                            </NuxtLink></span>

                        <div class="price">
                            <h3 v-if="product.discount > 0">{{ (Math.floor(product.price - ((product.price *
                                product.discount) /
                                100))).toLocaleString() + ' ₸' }}</h3>
                            <h3 v-else>{{ product.price == 0 ? 'Бесплатно' : product.price.toLocaleString() + ' ₸' }}</h3>
                            <button @click="addToCart()" v-if="accType == 'buyer' || accType == ''" ref="cartBtn">добавить в
                                корзину</button>
                        </div>
                    </div>
                </div>
                <div class="product__author">
                    <span>Продавец: <NuxtLink :to='"/seller/" + seller.id'>{{ seller.user.first_name }}
                        </NuxtLink></span>
                </div>
            </div>

            <div class="similar__products">
                <h1>похожие товары</h1>

                <div class="similar__body">
                    <NuxtLink v-for="item in product.similar_products" :to="'/product/' + item.id" class="similar__block">
                        <img :src="pathUrl + '/api' + item.add_image[0]" alt="">

                        <h1>{{ item.name }}</h1>

                        <div class="price">
                            <div>
                                <span v-if="item.discount > 0">{{ (Math.floor(item.price - ((item.price * item.discount) /
                                    100))).toLocaleString() + ' ₸' }}</span>
                                <span v-else>{{ item.price == 0 ? 'Бесплатно' : item.price.toLocaleString() + ' ₸' }}</span>
                                <small v-if="item.discount > 0">{{ item.price.toLocaleString() + ' ₸' }}</small>
                            </div>

                            <p class="mb-0" v-if="item.discount > 0">-{{ item.discount }}%</p>
                        </div>
                    </NuxtLink>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import { Navigation } from 'swiper/modules';
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';
import global from '~/mixins/global';
import axios from 'axios';
export default {
    mixins: [global],
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
            productId: this.$route.params.id,
            product: [],
            seller: [],
            pathUrl: 'https://merchshop.kz',
            category: '',
            rating: null,
            count: null,
            accType: '',
        }
    },
    computed: {
        filteredImages() {
            return this.product.add_image.slice(1);
        }
    },
    methods: {
        addToCart() {
            const path = `${this.pathUrl}/api/buyer/add-product-basket`
            const csrf = this.getCSRFToken()
            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            axios
                .post(path, {
                    products: this.product.id,
                    amount: 1,
                })
                .then(response => {
                    if (response.status == 201) {
                        this.$refs.cartBtn.innerHTML = 'Добавлен'
                        this.$refs.cartBtn.disabled = true
                        this.$refs.cartBtn.classList.add('disabled')
                    }
                    else {
                        this.$refs.cartBtn.innerHTML = 'Ошибка'
                        this.$refs.cartBtn.disabled = false

                    }
                    console.log(response)
                })
                .catch(error => {
                    console.error(error)
                })
        },
        getProduct() {
            const path = `${this.pathUrl}/api/products/detail-product/${this.productId}`
            axios
                .get(path)
                .then(response => {
                    this.product = response.data
                    this.seller = response.data.seller
                    this.rating = response.data.seller.rating
                    this.category = response.data.category.category_name
                    this.count = response.data.seller.amount_products
                })
                .catch(error => {
                    console.error(error)
                })
        },
    },
    mounted() {
        this.getProduct()

        const accType = localStorage.getItem('accountType')
        if (accType == 'buyer-account') {
            this.accType = 'buyer'
        }
        else if (accType == 'seller-account') {
            this.accType = 'seller'
        }
        else {
            this.accType = ''
            console.log('not authorized')
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