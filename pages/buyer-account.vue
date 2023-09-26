<template>
    <div class="account">

        <h1>личный кабинет</h1>

        <div class="navs">
            <div>
                <button @click="activeTab = 0" :class="{ activeTab: activeTab == 0 }">История покупок</button>
                <button @click="activeTab = 1" :class="{ activeTab: activeTab == 1 }">транзакции</button>
            </div>
            <div>
                <button @click="activeTab = 2" :class="{ activeTab: activeTab == 2 || activeTab == 7 }">обратная
                    связь</button>
                <button @click="activeTab = 3" :class="{ activeTab: activeTab == 3 }">аккаунт</button>
            </div>
        </div>

        <div class="myBuys" v-if="activeTab == 0">
            <swiper :slides-per-view="4" :auto-height="true" :space-between="30" :breakpoints="breakpoints"
                :modules="modules" :navigation="navigation2">
                <swiper-slide class="slide">
                    <div class="images">
                        <img src="@/assets/img/slide1.png" alt="">
                        <img src="@/assets/img/slide2.png" alt="">
                        <img src="@/assets/img/slide3.png" alt="">
                    </div>

                    <h1>ЗАКАЗ №383027</h1>
                    <span>ДАТА Покупки: 05.09.2023</span>
                    <h1>19 070 ₸</h1>

                    <button>ЧАТ С Продавцом</button>
                </swiper-slide>
                <swiper-slide class="slide">
                    <div class="images">
                        <img src="@/assets/img/slide1.png" alt="">
                        <img src="@/assets/img/slide2.png" alt="">
                        <img src="@/assets/img/slide3.png" alt="">
                    </div>

                    <h1>ЗАКАЗ №383027</h1>
                    <span>ДАТА Покупки: 05.09.2023</span>
                    <h1>19 070 ₸</h1>

                    <button>ЧАТ С Продавцом</button>
                </swiper-slide>
                <swiper-slide class="slide">
                    <div class="images">
                        <img src="@/assets/img/slide1.png" alt="">
                        <img src="@/assets/img/slide2.png" alt="">
                        <img src="@/assets/img/slide3.png" alt="">
                    </div>

                    <h1>ЗАКАЗ №383027</h1>
                    <span>ДАТА Покупки: 05.09.2023</span>
                    <h1>19 070 ₸</h1>

                    <button>ЧАТ С Продавцом</button>
                </swiper-slide>
                <swiper-slide class="slide">
                    <div class="images">
                        <img src="@/assets/img/slide1.png" alt="">
                        <img src="@/assets/img/slide2.png" alt="">
                        <img src="@/assets/img/slide3.png" alt="">
                    </div>

                    <h1>ЗАКАЗ №383027</h1>
                    <span>ДАТА Покупки: 05.09.2023</span>
                    <h1>19 070 ₸</h1>

                    <button>ЧАТ С Продавцом</button>
                </swiper-slide>

            </swiper>
            <div class="swipernavs">
                <img src="@/assets/img/prev.svg" class="prev" alt="">
                <img src="@/assets/img/next.svg" class="next" alt="">
            </div>
        </div>
        <div class="chats" v-if="activeTab == 2">
            <div class="chat__item">
                <div>
                    <h2>alex.ivanov@gmail.com</h2>
                    <small>23.07.2023 14:47</small>
                </div>

                <div class="justify-content-end">
                    <button @click="activeTab = 7">Открыть чат</button>
                </div>
            </div>
            <div class="chat__item">
                <div>
                    <h2>alex.ivanov@gmail.com</h2>
                    <small>23.07.2023 14:47</small>
                </div>

                <div class="justify-content-end">
                    <button>Открыть чат</button>
                </div>
            </div>
            <div class="chat__item">
                <div>
                    <h2>alex.ivanov@gmail.com</h2>
                    <small>23.07.2023 14:47</small>
                </div>

                <div class="justify-content-end">
                    <button>Открыть чат</button>
                </div>
            </div>
        </div>

        <div class="acc__info" v-if="activeTab == 3">
            <div>
                <label for="email">Эл.почта</label>
                <input type="email" v-model="email" placeholder="Эл.почта">
                <div class="text-right">
                    <button>сохранить изменения</button>
                </div>
            </div>
            <div>
                <label for="password">Пароль</label>
                <input type="password" placeholder="Пароль">
                <div class="text-left">
                    <button>выйти из аккаунта</button>
                </div>
            </div>
        </div>

        <TheTrans v-if="activeTab == 1" :transactions="transactions"></TheTrans>
        <TheMessanger v-if="activeTab == 7" :chatId="chatId" :name="chatName"></TheMessanger>
    </div>
</template>
<script>
import { Navigation } from 'swiper/modules';
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';
export default {
    data() {
        return {
            email: '',
            activeTab: 0,
            transactions: [],
            modules: [Navigation],
            navigation2: {
                nextEl: '.next',
                prevEl: '.prev',
            },

            breakpoints: {
                320: {
                    slidesPerView: 1,
                    spaceBetween: 10,

                },
                1300: {
                    slidesPerView: 3,
                    spaceBetween: 30,
                }
            },
        }
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Личный кабинет | MerchShop',
    ogTitle: 'Личный кабинет | MerchShop',
    description: 'Личный кабинет | MerchShop',
    ogDescription: 'Личный кабинет | MerchShop',
})
</script>
<style lang="scss" scoped>
.account {
    padding: 150px 100px 60px;

    .acc__info {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 50px;
        margin: 10.417vw 0;

        label,
        input {
            display: block;
        }

        label {
            margin-bottom: 10px;
            font-size: 16px;
            font-style: normal;
            font-weight: 500;
            line-height: 110%;
            font-family: var(--int);
            color: #000;
        }

        input {
            border: 2px solid #D2D2D2;
            background: transparent;
            padding: 10px;

            font-size: 16px;
            font-style: normal;
            font-weight: 400;
            line-height: 130%;
            font-family: var(--int);
            color: #000;
            width: 23.438vw;
        }

        button {
            border: 2px solid #D2D2D2;
            background: transparent;
            padding: 10px 20px;

            font-size: 16px;
            font-style: normal;
            font-weight: 500;
            line-height: normal;
            text-transform: uppercase;
            font-family: var(--int);
            color: #000;
            margin-top: 50px;
        }
    }

    .chats {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(546px, 1fr));
        gap: 41px;
        grid-auto-flow: dense;
        margin-top: 40px;

        .chat__item {
            background: #fff;
            padding: 30px 20px;
            border: 2px solid #D2D2D2;

            div {
                display: flex;
                justify-content: space-between;
                align-items: center;

                h2,
                small {
                    margin: 0;
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: normal;
                    font-family: var(--int);
                    color: #000;
                }

                button {
                    margin-top: 30px;
                    padding: 10px 30px;
                    background: transparent;
                    border: 2px solid #D2D2D2;

                    font-size: 16px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;
                }
            }
        }
    }

    .myBuys {
        display: flex;
        gap: 15px;
        margin-top: 33px;

        .swipernavs {
            display: flex;
            gap: 20px;

            img {
                cursor: pointer;
            }
        }

        .slide {
            border: 2px solid #D2D2D2;
            background: #fff;
            padding: 30px 40px;
            width: 510px !important;

            h1 {
                margin: 20px 0;
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: normal;
                text-transform: uppercase;
                font-family: var(--int);
                color: #000;
            }

            span {
                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: normal;
                text-transform: uppercase;
                font-family: var(--int);
                color: #000;
            }

            button {
                padding: 10px 20px;
                background: transparent;
                border: 2px solid #D2D2D2;

                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: normal;
                text-transform: uppercase;
                font-family: var(--int);
                color: #000;
            }

            .images {
                display: flex;
                gap: 20px;

                img {
                    width: 130px;
                    height: 130px;
                    object-fit: cover;
                }
            }
        }
    }

    .navs {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 30px;

        .activeTab {
            background: #fff;
        }

        div {
            display: flex;
            gap: 30px;

            button {
                padding: 10px 20px;
                background: transparent;
                border: 2px solid #828282;

                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                /* 20.8px */
                text-transform: uppercase;
                font-family: var(--int);
                color: #000;
                transition: all .3s ease;
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
        margin: 0 0 30px;
    }
}
</style>