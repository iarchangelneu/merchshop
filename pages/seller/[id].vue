<template>
    <div v-if="author.length <= 0"></div>
    <div class="seller" v-else>
        <PrevPage></PrevPage>
        <h1>{{ author.user.first_name }}</h1>

        <div class="seller__info">
            <img :src="author.photo" alt="">

            <div class="seller__desc">
                <h2>Описание:</h2>

                <div v-html="author.description"></div>
            </div>
        </div>

        <div class="seller__products">
            <h1>товары продавца</h1>

            <div class="similar__body">
                <NuxtLink v-for=" item  in  author.products " :to="'/product/' + item.id" class="similar__block">
                    <img :src="item.add_image[0].image" alt="">

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
</template>
<script>
import global from '~/mixins/global';
import axios from 'axios';
export default {
    mixins: [global],
    data() {
        return {
            productId: this.$route.params.id,
            author: [],
            pathUrl: 'https://merchshop.kz',
            products: [],
            description: 'Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание'
        }
    },
    methods: {
        getAuthor() {
            const path = `${this.pathUrl}/api/seller/seller-this/${this.productId}`
            axios
                .get(path)
                .then(response => {
                    this.author = response.data
                    this.products = response.data.products

                })
                .catch(error => {
                    console.error(error)
                })
        }
    },
    mounted() {
        this.getAuthor()
    }
}
</script>
<script setup>

useSeoMeta({
    title: 'Страница продавца | MerchShop',
    ogTitle: 'Страница продавца | MerchShop',
    description: 'Страница продавца | MerchShop',
    ogDescription: 'Страница продавца | MerchShop',
})
</script>
<style lang="scss" scoped>
.seller {
    padding: 150px 100px 60px;

    @media (max-width: 1600px) {
        padding: 150px 50px 60px;
    }

    @media (max-width: 1024px) {
        padding: 100px 20px 60px;
    }

    .seller__products {
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
                    margin-top: auto;
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
            margin: 30px 0;
        }
    }

    .seller__info {
        display: flex;
        gap: 30px;
        align-items: flex-start;

        @media (max-width: 1024px) {
            flex-direction: column;
            gap: 20px;
            width: 100%;
        }

        .seller__desc {
            div {
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                max-width: 1113px;
            }

            h2 {
                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: 110%;
                font-family: var(--int);
                color: #000;
                margin-bottom: 10px;
            }
        }

        img {
            width: 320px;
            height: 275px;
            object-fit: cover;

            @media (max-width: 1024px) {
                width: 100%;
                height: 300px;
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

        @media (max-width: 1024px) {
            font-size: 20px;
        }
    }
}
</style>