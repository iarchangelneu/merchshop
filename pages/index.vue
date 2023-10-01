<template>
    <div class="main">
        <div class="main__body">
            <div class="main__block text-center">
                <img class="img-fluid mainpc" src="@/assets/img/main.png" alt="">
                <img src="@/assets/img/mainmob.svg" class="mainmob" alt="">
                <h2>Подарки для себя и близких</h2>
                <h1>Подарки для себя и близких</h1>
                <h3>merchshop.kz - помощник на все знаковые события </h3>

                <div class="text-right">
                    <NuxtLink to="/catalog">каталог</NuxtLink>
                </div>
            </div>
        </div>
    </div>

    <div class="line">
        <div class="running-text">
            <div class="text-container">
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
                <div class="divider">•</div>
                <div class="text-segment">АКЦИИ</div>
                <div class="divider">•</div>
                <div class="text-segment">СКИДКИ</div>
            </div>
        </div>
    </div>

    <div class="page">
        <div class="sales">
            <h1>Акции и скидки</h1>

            <div class="sales__body">
                <div class="sales__row">
                    <NuxtLink class="sales__block" v-for="item in discounts.slice(0, 4)" :key="item.id"
                        :to="'/product/' + item.id">
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
                <div class="sales__row">
                    <NuxtLink class="sales__block" v-for="item in discounts.slice(4, 8)" :key="item.id"
                        :to="'/product/' + item.id">
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
            <div class="text-right">
                <NuxtLink to="/catalog">
                    ПОСМОТРЕТЬ ВСЕ
                </NuxtLink>
            </div>
        </div>

        <div class="categories">
            <h1>категории</h1>

            <div class="categories__body">
                <NuxtLink to="/catalog/?category=1" class="categories__block">
                    <img src="@/assets/img/cat1.png" alt="">

                    <h1>сТИКЕРЫ</h1>
                </NuxtLink>
                <NuxtLink to="/catalog/?category=2" class="categories__block">
                    <img src="@/assets/img/cat2.png" alt="">
                    <h1>ОДЕЖДА</h1>
                </NuxtLink>
                <NuxtLink to="/catalog/?category=3" class="categories__block">
                    <img src="@/assets/img/cat3.png" alt="">
                    <h1>ЧЕХЛЫ НА ТЕЛЕФОН</h1>
                </NuxtLink>
                <NuxtLink to="/catalog/?category=4" class="categories__block">
                    <img src="@/assets/img/cat4.png" alt="">
                    <h1>ПОСТЕРЫ</h1>
                </NuxtLink>
                <NuxtLink to="/catalog/?category=5" class="categories__block">
                    <img src="@/assets/img/cat5.png" alt="">
                    <h1>ДЛЯ ДОМА</h1>
                </NuxtLink>
                <NuxtLink to="/catalog/?category=6" class="categories__block">
                    <img src="@/assets/img/cat6.png" alt="">
                    <h1>АКСЕССУАРЫ</h1>
                </NuxtLink>
                <NuxtLink to="/catalog/?category=7" class="categories__block">
                    <img src="@/assets/img/cat7.png" alt="">
                    <h1>ДЛЯ ПИТОМЦЕВ</h1>
                </NuxtLink>
                <NuxtLink to="/catalog/?category=8" class="categories__block">
                    <img src="@/assets/img/cat8.png" alt="">
                    <h1>КАНЦЕЛЯРИЯ</h1>
                </NuxtLink>
                <NuxtLink to="/catalog/?category=9" class="categories__block">
                    <img src="@/assets/img/cat9.png" alt="">
                    <h1>ДЛЯ ДЕТЕЙ</h1>
                </NuxtLink>
                <NuxtLink to="/catalog/?category=10" class="categories__block">
                    <img src="@/assets/img/cat10.png" alt="">
                    <h1>ПОДАРОЧНЫЕ НАБОРЫ</h1>
                </NuxtLink>
            </div>
        </div>


        <div class="sales">
            <h1>Популярное</h1>

            <div class="sales__body">
                <div class="sales__row">
                    <NuxtLink class="sales__block" v-for="item in populars.slice(0, 4)" :key="item.id"
                        :to="'/product/' + item.id">
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
                <div class="sales__row">
                    <NuxtLink class="sales__block" v-for="item in populars.slice(4, 8)" :key="item.id"
                        :to="'/product/' + item.id">
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
            <div class="text-right">
                <NuxtLink to="/catalog">
                    ПОСМОТРЕТЬ ВСЕ
                </NuxtLink>
            </div>
        </div>


        <div class="about">
            <div class="white"></div>
            <div class="yellow"></div>
            <div class="purple">
                <div>
                    <h1>О НАС</h1>
                    <p>Добро пожаловать в «merchshop.kz» — ваш уникальный маркетплейс, где стиль и креативность встречаются
                        в разнообразии товаров! Мы гордимся представлять вам бесконечное разнообразие уникальных продуктов,
                        включая стильные футболки, яркие стикеры, оригинальные кружки и многое другое.</p>

                    <NuxtLink to="/about">ПОДРОБНЕЕ</NuxtLink>
                </div>

                <img src="@/assets/img/about.png" class="img-fluid" alt="">
            </div>
        </div>


        <div class="reviews">
            <h1>Отзывы</h1>

            <div class="reviews__slider">
                <swiper :slides-per-view="4" :auto-height="true" :space-between="27" :breakpoints="breakpoints"
                    :modules="modules" :navigation="navigation">
                    <swiper-slide class="slide">
                        <h1>обожаю merchshop</h1>

                        <p>Обожаю Merchshop, все мои близкие получают отличные подарки на праздники именно отсюда. Люблю!
                        </p>

                        <div class="text-right">
                            <small>Катя</small>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="slide">
                        <h1>это не просто магазин</h1>

                        <p>Это место, где можно найти вдохновение. Я часто заглядываю сюда, чтобы найти мотивацию. Спасибо!
                        </p>

                        <div class="text-right">
                            <small>Лиза</small>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="slide">
                        <h1>стикеры отпад</h1>

                        <p>Моя коллекция стикеров стала поистине впечатляющей! Я нашел стикеры на самые разные темы и стили,
                            которые придают моим вещам неповторимый вид.
                        </p>

                        <div class="text-right">
                            <small>Николай</small>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="slide">
                        <h1>merchshop лучший</h1>

                        <p>Он сделал покупку товаров простой и приятной. Я частый гость здесь в поисках новых предметов
                            для своей коллекции. Великолепное место для настоящих ценителей
                        </p>

                        <div class="text-right">
                            <small>Марина</small>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="slide">
                        <h1>обожаю merchshop</h1>

                        <p>Обожаю Merchshop, все мои близкие получают отличные подарки на праздники именно отсюда. Люблю!
                        </p>

                        <div class="text-right">
                            <small>Катя</small>
                        </div>
                    </swiper-slide>



                </swiper>
                <div class="text-right mt-4">
                    <img src="@/assets/img/prev.svg" class="prev" alt="">
                    <img src="@/assets/img/next.svg" class="next ml-4" alt="">
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
                    spaceBetween: 30,
                }
            },
            pathUrl: 'https://merchshop.kz',
            populars: [],
            discounts: [],
        }
    },
    methods: {
        getPopulars() {
            const path = `${this.pathUrl}/api/products/popular-product?amount_products=8`;
            axios
                .get(path)
                .then(response => {
                    this.populars = response.data
                })
                .catch(error => {
                    console.log(error)
                })
        },
        getDiscount() {
            const path = `${this.pathUrl}/api/products/discount-product?amount_products=8`;
            axios
                .get(path)
                .then(response => {
                    this.discounts = response.data
                })
                .catch(error => {
                    console.log(error)
                })
        },
    },
    mounted() {
        this.getPopulars()
        this.getDiscount()
    },

}
</script>
<script setup>
useSeoMeta({
    title: 'Главная | MerchShop',
    ogTitle: 'Главная | MerchShop',
    description: 'Главная | MerchShop',
    ogDescription: 'Главная | MerchShop',
})
</script>
<style lang="scss" scoped>
.page {
    padding: 0 100px 10px;

    @media (max-width: 1600px) {
        padding: 0 50px 10px;
    }

    @media (max-width: 1024px) {
        padding: 0 20px 60px;
    }

    .reviews {
        margin-top: 10px;
        padding: 30px 20px;
        border-radius: 20px;
        border: 2px solid #D2D2D2;

        @media (max-width: 1024px) {
            border: 0;
            padding: 0;

        }


        .reviews__slider {


            .slide {
                display: flex;
                flex-direction: column;
                height: 215px;

                padding: 20px 20px 15px;
                // background: url('@/assets/img/tex.svg'), lightgray 0% 0% / 40.00000059604645px 40.00000059604645px repeat;
                background-color: #F7BFCA;
                border-radius: 20px;

                h1 {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 600;
                    line-height: 150%;
                    /* 30px */
                    text-transform: uppercase;
                    font-family: var(--int);
                    color: #fff;
                    margin-bottom: 10px;

                    @media (max-width: 1024px) {
                        font-size: 16px;
                    }
                }

                p {
                    font-size: 16px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 150%;
                    font-family: var(--int);
                    color: #000;
                    max-width: 360px;
                    margin: 0;
                }

                .text-right {
                    margin-top: auto;
                }

                small {
                    margin-top: auto;
                    font-size: 16px;
                    font-style: normal;
                    font-weight: 600;
                    line-height: 150%;
                    font-family: var(--int);
                    color: #fff;
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
            margin-bottom: 22px;

            @media (max-width: 1024px) {
                font-size: 20px;
            }
        }

    }

    .about {
        position: relative;
        margin-top: 10px;
        height: 550px;

        @media (max-width: 1200px) {
            height: 360px;
        }

        @media (max-width: 1024px) {
            height: 550px;
        }

        .white {
            position: absolute;
            right: 0;
            background: #fff;
            border-radius: 20px;
            border: 2px solid #D2D2D2;
            height: 489px;
            width: 86.458vw;
            z-index: 1;

            @media (max-width: 1200px) {
                height: 300px;
            }

            @media (max-width: 1024px) {
                width: 85vw;
            }

            @media (max-width: 500px) {
                height: 490px;
                width: 310px;
            }
        }

        .yellow {
            position: absolute;
            right: 30px;
            top: 30px;
            background: #FDED01;
            border-radius: 20px;
            border: 2px solid #D2D2D2;
            height: 489px;
            width: 86.458vw;
            z-index: 2;

            @media (max-width: 1200px) {
                height: 300px;
            }

            @media (max-width: 1024px) {
                width: 85vw;
            }

            @media (max-width: 500px) {
                height: 490px;
                width: 310px;
                top: 20px;
                right: 20px;
            }
        }

        .purple {
            display: flex;
            justify-content: space-between;
            padding: 30px 100px 20px 30px;

            position: absolute;
            right: 60px;
            top: 60px;
            // background: url('@/assets/img/tex.svg'), lightgray 0% 0% / 40.00000059604645px 40.00000059604645px repeat;
            background-color: #F7BFCA;
            z-index: 3;
            border-radius: 20px;
            border: 0;
            height: 489px;
            width: 86.458vw;

            @media (max-width: 1200px) {
                height: 300px;
            }

            @media (max-width: 1024px) {
                width: 85vw;
            }

            @media (max-width: 500px) {
                height: 490px;
                width: 310px;
                padding: 20px 20px 30px;
                right: 40px;
                top: 40px;
            }

            img {
                @media (max-width: 1430px) {
                    max-width: 50% !important;
                    height: auto;
                }

                @media (max-width: 1200px) {
                    display: none;
                }
            }


            h1 {
                font-size: 40px;
                font-style: normal;
                font-weight: 600;
                line-height: normal;
                font-family: var(--int);
                color: #000;
                margin-bottom: 22px;

                @media (max-width: 1430px) {
                    font-size: 35px;
                }

                @media (max-width: 1024px) {
                    font-size: 20px;
                }

            }

            p {
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 150%;
                text-transform: uppercase;
                font-family: var(--int);
                color: #000;
                margin-bottom: 20px;
                max-width: 832px;

                @media (max-width: 1430px) {
                    font-size: 16px;
                }

                @media (max-width: 1024px) {
                    font-size: 16px;
                    max-width: none;
                }


            }

            a {
                text-decoration: none;
                border: 2px solid #000;
                padding: 10px 20px;

                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: normal;
                text-transform: uppercase;
                font-family: var(--int);
                color: #000;
            }
        }
    }

    .categories {
        margin-top: 10px;
        padding: 30px 20px 80px;
        border-radius: 20px;
        border: 2px solid #D2D2D2;

        @media (max-width: 1024px) {
            border: 0;
            padding: 0;
            margin-top: 20px;
        }

        .categories__body {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
            grid-auto-flow: dense;

            a {
                text-decoration: none;
            }

            @media (max-width: 1024px) {
                grid-template-columns: repeat(auto-fill, minmax(165px, 1fr));
            }


            .categories__block {
                display: flex;
                flex-direction: column;

                padding: 10px;
                border: 1px solid #D2D2D2;
                background: #fff;

                img {
                    width: 100%;
                    height: 290px;
                    object-fit: cover;

                    @media (max-width: 1024px) {
                        height: 130px;
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
                    margin-top: 10px;

                    @media (max-width: 1024px) {
                        font-size: 10px;
                        margin-bottom: 10px;
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
            margin-bottom: 22px;

            @media (max-width: 1024px) {
                font-size: 20px;
            }
        }
    }

    .sales {
        margin-top: 10px;
        padding: 30px 20px 20px;
        border-radius: 20px;
        border: 2px solid #D2D2D2;

        @media (max-width: 1024px) {
            border: 0;
            padding: 0;
            margin-top: 20px;
        }

        a {
            font-size: 16px;
            font-style: normal;
            font-weight: 500;
            line-height: normal;
            text-transform: uppercase;
            font-family: var(--int);
            text-decoration: none;
            color: #000;

            padding: 10px 20px;
            background: transparent;
            border: 1px solid #D2D2D2;

            @media (max-width: 1024px) {
                display: none;
            }
        }

        .sales__body {



            .sales__row {
                display: flex;
                gap: 32px;
                margin-bottom: 30px;

                @media (max-width: 1800px) {
                    display: grid;
                    grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
                    gap: 35px;
                    grid-auto-flow: dense;
                }

                @media (max-width: 1024px) {
                    gap: 20px;
                    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
                    margin-bottom: 20px;
                }

                @media (max-width: 830px) {
                    gap: 20px;
                    grid-template-columns: repeat(auto-fill, minmax(165px, 1fr));
                    margin-bottom: 20px;
                }

                .sales__block {
                    background: #fff;
                    text-decoration: none;
                    border: 1px solid #D2D2D2;
                    padding: 10px;
                    display: flex;
                    flex-direction: column;
                    max-width: 340px;

                    @media (max-width: 1800px) {
                        max-width: 100%;
                    }

                    &:last-child {
                        max-width: 560px;

                        @media (max-width: 1800px) {
                            max-width: 100%;
                            display: none;
                        }

                        @media (max-width: 1250px) {
                            display: flex;
                        }

                        @media (max-width: 1024px) {
                            display: none;
                        }

                        @media (max-width: 830px) {
                            display: flex;
                        }

                        img {
                            width: 540px;
                            height: 290px;
                            object-fit: cover;

                            @media (max-width: 1800px) {
                                width: 100%;
                                height: 290px;
                            }

                            @media (max-width: 1024px) {
                                height: 130px;
                            }
                        }
                    }

                    img {
                        width: 320px;
                        height: 290px;
                        object-fit: cover;

                        @media (max-width: 1800px) {
                            width: 100%;
                        }

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
                                    font-size: 12px;
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
        }

        h1 {
            font-size: 40px;
            font-style: normal;
            font-weight: 600;
            line-height: normal;
            text-transform: uppercase;
            font-family: var(--int);
            color: #000;
            margin-bottom: 22px;

            @media (max-width: 1024px) {
                font-size: 20px;
            }
        }
    }
}

.line {
    background: #FDED01;
    // overflow: hidden;
}

.running-text {
    min-height: 40px;
    width: 100%;
    position: relative;
    padding-top: 7px;
    white-space: nowrap;
}

.text-container {
    display: flex;
    animation: marquee 45s linear infinite;
}

.text-segment {
    margin-right: 15px;
    font-size: 16px;
    font-style: normal;
    font-weight: 600;
    line-height: normal;
    text-transform: uppercase;
    font-family: var(--int);
    color: #000;
}

.divider {
    margin-right: 15px;
}

@keyframes marquee {
    0% {
        transform: translateX(0);
    }

    100% {
        transform: translateX(calc(-100% + 1rem));
    }
}

.main {
    padding: 150px 100px 10px;

    @media (max-width: 1600px) {
        padding: 150px 50px 10px;
    }

    @media (max-width: 1024px) {
        padding: 100px 20px 10px;
    }

    .main__body {
        opacity: 0.8;
        border-radius: 20px;
        //  mix-blend-mode: overlay;
        // background: url('@/assets/img/tex.svg'), lightgray 0% 0% / 40.00000059604645px 40.00000059604645px repeat;
        background-color: #F7BFCA;

        //   height: 100vh;

        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;

        padding: 77px 111px;

        @media (max-width: 1024px) {
            padding: 0 10px 33px;
        }

        .main__block {
            position: relative;
            width: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;

            .mainmob {
                display: none;
                align-items: center;
                width: 100%;

                @media (max-width: 1024px) {
                    display: block;
                }
            }

            .mainpc {
                display: block;

                @media (max-width: 1024px) {
                    display: none;
                }
            }

            h1 {
                font-size: 57px;
                font-style: normal;
                font-weight: 600;
                line-height: normal;
                font-family: var(--pr);
                color: #000;
                z-index: 1;

                position: absolute;
                top: 50%;
                //white-space: nowrap;
                width: 100%;

                @media (max-width: 1024px) {
                    position: absolute;
                    font-size: 20px;
                    font-weight: 600;
                    top: 85.7vw;
                }

                @media (max-width: 750px) {
                    top: 84.5vw;
                }

                @media (max-width: 450px) {
                    top: 80vw;
                }
            }

            h2 {
                font-size: 57px;
                font-style: normal;
                font-weight: 400;
                line-height: normal;
                font-family: var(--pr);
                color: #fff;
                z-index: 2;

                position: absolute;
                top: 50%;
                //white-space: nowrap;
                width: 100%;

                @media (max-width: 1024px) {
                    position: relative;
                    font-size: 20px;
                    margin-top: 20px;
                    font-weight: 400;
                }
            }

            h3 {
                font-size: 12px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                text-transform: uppercase;
                font-family: var(--int);
                color: #fff;
                max-width: 188px;

                position: absolute;
                top: 40%;
                left: 15%;

                @media (max-width: 1024px) {
                    position: relative;
                    text-align: center;
                    top: 0;
                    left: 0;
                    margin-top: 20px;
                }
            }

            a {
                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: normal;
                text-transform: uppercase;
                font-family: var(--int);
                color: #fff;
                text-decoration: none;
                transition: all .3s ease;


                padding: 10px 20px;
                background: transparent;
                border: 2px solid #fff;

                position: absolute;
                bottom: 5%;
                right: 0%;

                @media (max-width: 1024px) {
                    position: relative;
                    margin-top: 20px;
                    display: inline-block;
                }

            }
        }
    }
}
</style>