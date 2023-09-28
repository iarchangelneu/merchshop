<template>
    <div class="account">

        <h1>личный кабинет</h1>

        <div class="navs">
            <div>
                <button @click="activeTab = 0"
                    :class="{ activeTab: activeTab == 0 || activeTab == 5 || activeTab == 6 }">мои
                    товары</button>
                <button @click="activeTab = 1" :class="{ activeTab: activeTab == 1 }">мои продажи</button>
            </div>
            <div>
                <button @click="activeTab = 2" :class="{ activeTab: activeTab == 2 }">транзакции</button>
                <button @click="activeTab = 3" :class="{ activeTab: activeTab == 3 || activeTab == 7 }">обратная
                    связь</button>
            </div>
            <div>
                <button @click="activeTab = 4" :class="{ activeTab: activeTab == 4 }">аккаунт</button>
            </div>
        </div>

        <div class="mysales" v-if="activeTab == 0">
            <div class="text-center">
                <button class="add__product" @click="activeTab = 5">
                    добавить товар
                </button>
            </div>
            <div class="sale__slider salesmob">
                <div class="slide">
                    <div class="images">
                        <img src="@/assets/img/sale3.png" alt="">
                        <img src="@/assets/img/sale3.png" alt="">
                        <img src="@/assets/img/sale3.png" alt="">
                    </div>

                    <h1>чехол на телефон</h1>
                    <h1>19 070 ₸</h1>

                    <div class="buttons">
                        <button @click="activeTab = 6">Изменить</button>
                        <NuxtLink to="/product/1">страница товара</NuxtLink>
                    </div>
                </div>
                <div class="slide">
                    <div class="images">
                        <img src="@/assets/img/sale3.png" alt="">
                        <img src="@/assets/img/sale3.png" alt="">
                        <img src="@/assets/img/sale3.png" alt="">
                    </div>

                    <h1>чехол на телефон</h1>
                    <h1>19 070 ₸</h1>

                    <div class="buttons">
                        <button @click="activeTab = 6">Изменить</button>
                        <NuxtLink to="/product/1">страница товара</NuxtLink>
                    </div>
                </div>
            </div>
            <div class="sale__slider salespc">
                <swiper :slides-per-view="4" :auto-height="true" :space-between="30" :breakpoints="breakpoints"
                    :modules="modules" :navigation="navigation2">
                    <swiper-slide class="slide">
                        <div class="images">
                            <img src="@/assets/img/sale3.png" alt="">
                            <img src="@/assets/img/sale3.png" alt="">
                            <img src="@/assets/img/sale3.png" alt="">
                        </div>

                        <h1>чехол на телефон</h1>
                        <h1>19 070 ₸</h1>

                        <div class="buttons">
                            <button @click="activeTab = 6">Изменить</button>
                            <NuxtLink to="/product/1">страница товара</NuxtLink>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="slide">
                        <div class="images">
                            <img src="@/assets/img/sale3.png" alt="">
                            <img src="@/assets/img/sale3.png" alt="">
                            <img src="@/assets/img/sale3.png" alt="">
                        </div>

                        <h1>чехол на телефон</h1>
                        <h1>19 070 ₸</h1>

                        <div class="buttons">
                            <button>Изменить</button>
                            <NuxtLink to="/product/1">страница товара</NuxtLink>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="slide">
                        <div class="images">
                            <img src="@/assets/img/sale3.png" alt="">
                            <img src="@/assets/img/sale3.png" alt="">
                            <img src="@/assets/img/sale3.png" alt="">
                        </div>

                        <h1>чехол на телефон</h1>
                        <h1>19 070 ₸</h1>

                        <div class="buttons">
                            <button>Изменить</button>
                            <NuxtLink to="/product/1">страница товара</NuxtLink>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="slide">
                        <div class="images">
                            <img src="@/assets/img/sale3.png" alt="">
                            <img src="@/assets/img/sale3.png" alt="">
                            <img src="@/assets/img/sale3.png" alt="">
                        </div>

                        <h1>чехол на телефон</h1>
                        <h1>19 070 ₸</h1>

                        <div class="buttons">
                            <button>Изменить</button>
                            <NuxtLink to="/product/1">страница товара</NuxtLink>
                        </div>
                    </swiper-slide>

                </swiper>
                <div class="swipernavs">
                    <img src="@/assets/img/prev.svg" class="prev" alt="">
                    <img src="@/assets/img/next.svg" class="next" alt="">
                </div>
            </div>
        </div>
        <div class="mysales" v-if="activeTab == 1">
            <div class="sale__slider salesmob">
                <div class="slide">
                    <div class="images">
                        <img src="@/assets/img/sale3.png" alt="">
                        <img src="@/assets/img/sale3.png" alt="">
                        <img src="@/assets/img/sale3.png" alt="">
                    </div>

                    <h1>ЗАКАЗ №383027</h1>
                    <span>ДАТА Продажи: 05.09.2023</span>
                    <h1>19 070 ₸</h1>

                    <div class="buttons">
                        <button @click="activeTab = 6">ЧАТ С Покупателем</button>
                    </div>
                </div>
            </div>
            <div class="sale__slider salespc">
                <swiper :slides-per-view="4" :auto-height="true" :space-between="30" :breakpoints="breakpoints"
                    :modules="modules" :navigation="navigation2">
                    <swiper-slide class="slide">
                        <div class="images">
                            <img src="@/assets/img/sale3.png" alt="">
                            <img src="@/assets/img/sale3.png" alt="">
                            <img src="@/assets/img/sale3.png" alt="">
                        </div>

                        <h1>ЗАКАЗ №383027</h1>
                        <span>ДАТА Продажи: 05.09.2023</span>
                        <h1>19 070 ₸</h1>

                        <div class="buttons">
                            <button @click="activeTab = 6">ЧАТ С Покупателем</button>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="slide">
                        <div class="images">
                            <img src="@/assets/img/sale3.png" alt="">
                            <img src="@/assets/img/sale3.png" alt="">
                            <img src="@/assets/img/sale3.png" alt="">
                        </div>

                        <h1>ЗАКАЗ №383027</h1>
                        <span>ДАТА Продажи: 05.09.2023</span>
                        <h1>19 070 ₸</h1>

                        <div class="buttons">
                            <button @click="activeTab = 6">ЧАТ С Покупателем</button>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="slide">
                        <div class="images">
                            <img src="@/assets/img/sale3.png" alt="">
                            <img src="@/assets/img/sale3.png" alt="">
                            <img src="@/assets/img/sale3.png" alt="">
                        </div>

                        <h1>ЗАКАЗ №383027</h1>
                        <span>ДАТА Продажи: 05.09.2023</span>
                        <h1>19 070 ₸</h1>

                        <div class="buttons">
                            <button @click="activeTab = 6">ЧАТ С Покупателем</button>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="slide">
                        <div class="images">
                            <img src="@/assets/img/sale3.png" alt="">
                            <img src="@/assets/img/sale3.png" alt="">
                            <img src="@/assets/img/sale3.png" alt="">
                        </div>

                        <h1>ЗАКАЗ №383027</h1>
                        <span>ДАТА Продажи: 05.09.2023</span>
                        <h1>19 070 ₸</h1>

                        <div class="buttons">
                            <button @click="activeTab = 6">ЧАТ С Покупателем</button>
                        </div>
                    </swiper-slide>


                </swiper>
                <div class="swipernavs">
                    <img src="@/assets/img/prev.svg" class="prev" alt="">
                    <img src="@/assets/img/next.svg" class="next" alt="">
                </div>
            </div>
        </div>
        <div class="chats" v-if="activeTab == 3">
            <div class="chat__item">
                <div>
                    <h2>alex.ivanov@gmail.com</h2>
                </div>

                <div class="justify-content-end">
                    <button @click="activeTab = 7">Открыть чат</button>
                </div>
            </div>

        </div>

        <div class="accs" v-if="activeTab == 4">
            <div class="account__profile">
                <div class="profile__left">
                    <div class="avatar w-100">
                        <div class="avik">
                            <label for="fileInput" class="editava ml-0" @click="openFileInput">
                                <span>Изменить фото</span>
                            </label>
                            <input type="file" id="fileInput" ref="fileInput" accept="image/*"
                                style="display: none !important;" @change="handleFileChange">
                            <!-- Используем avatarUrl для отображения выбранного изображения или дефолтного изображения -->
                            <img :src="avatarUrl" alt="" loading="lazy">
                        </div>

                    </div>
                    <div class="data">
                        <label for="name">Отображаемое Имя</label>
                        <input type="text" placeholder="Ваше имя" class="w-100" v-model="name">
                    </div>
                    <div class="data">
                        <label for="name">E-mail</label>
                        <input class="w-100" type="email" placeholder="E-mail" v-model="email">
                    </div>

                    <div class="data">
                        <label for="name">Пароль</label>
                        <input class="w-100" type="password" placeholder="Пароль">
                    </div>

                </div>
                <div class="profile__right w-100">
                    <label for="desc">Описание профиля</label>
                    <textarea name="desc" id="desc" cols="30" rows="17" v-model="description"></textarea>


                    <div class="buttons">
                        <button @click="editAccount()" ref="edit">Сохранить изменения</button>
                        <button @click="logOut()">Выйти из аккаунта</button>
                    </div>
                </div>
            </div>
        </div>

        <TheTrans v-if="activeTab == 2" :transactions="transactions"></TheTrans>
        <CreateProduct v-if="activeTab == 5"></CreateProduct>
        <EditProduct v-if="activeTab == 6" :productId="sendId"></EditProduct>
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
            transactions: [],
            sendId: null,
            chatId: null,
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
<style lang="scss">
.account {
    padding: 150px 100px 60px;

    @media (max-width: 1600px) {
        padding: 150px 50px 60px;
    }

    @media (max-width: 1024px) {
        padding: 150px 20px 60px;
    }

    .accs {
        .buttons {
            display: flex;
            justify-content: flex-start;
            align-items: center;
            gap: 20px;
            margin-top: 30px;

            @media (max-width: 1024px) {
                flex-direction: column;
                align-items: flex-start;

            }

            button,
            a {
                padding: 10px 20px;
                border: 2px solid #D2D2D2;
                border-radius: 0;
                background: transparent;

                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                text-transform: uppercase;
                color: #000;
                transition: all .3s ease;


                @media (max-width: 1024px) {
                    flex: 1;
                }
            }
        }
    }

    .account__profile {
        margin-top: 38px;
        display: flex;
        gap: 54px;

        @media (max-width: 1024px) {
            flex-direction: column;
            margin-top: 20px;
        }

        label,
        input {
            display: block;
        }

        label {
            font-size: 16px;
            font-style: normal;
            font-weight: 500;
            line-height: 110%;
            font-family: var(--int);
            color: #000;
            margin-left: 10px;
        }

        input {
            border: 2px solid #D2D2D2;
            border-radius: 0;
            padding: 10px;
            width: 336px;

            font-size: 16px;
            font-style: normal;
            font-weight: 400;
            line-height: 130%;
            font-family: var(--int);
            color: #000;
            background: transparent;

            @media (max-width: 1024px) {
                width: 100%;
                max-width: 100%;
                display: inline;
            }
        }


        .profile__left {
            //  width: 100%;

            .data {
                margin-top: 20px;
            }

            .avatar {
                display: flex;
                gap: 20px;
                align-items: flex-start;

                @media (max-width: 1024px) {
                    flex-direction: column;
                    align-items: center;
                    width: 100%;
                }

                .avik {
                    border-radius: 0;
                }

                img {
                    width: 16.667vw;
                    height: 14.323vw;
                    object-fit: cover;

                    @media (max-width: 1024px) {
                        width: 100%;
                        height: 300px;
                    }
                }

                div {
                    position: relative;
                    overflow: hidden;

                    &:last-child {
                        @media (max-width: 1024px) {
                            width: 100%;
                        }
                    }



                    .editava {
                        position: absolute;
                        display: flex !important;
                        justify-content: center;
                        align-items: center;
                        transition: all .3s ease;
                        transform: scaleY(0);
                        width: 100%;
                        height: 100%;
                        border-radius: 0;
                        background: rgba(246, 246, 246, 0.30);
                        cursor: pointer;

                        top: 0;

                        span {
                            display: flex;
                            align-items: center;
                            justify-content: center;
                            padding: 10px;
                            background: #fff;
                            border-radius: 0;

                            font-size: 10.755px;
                            font-style: normal;
                            font-weight: 500;
                            line-height: 130%;
                            text-decoration-line: underline;
                            font-family: var(--int);
                            color: #000;
                            cursor: pointer;
                        }

                    }

                    &:hover .editava {
                        transform: scaleY(1)
                    }
                }
            }
        }

        .profile__right {
            textarea {
                width: 100%;
                // max-width: ;
                display: block;
                background: transparent;
                border-radius: 0;
                border: 2px solid #D2D2D2;
                padding: 20px;

                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
            }
        }
    }

    .chats {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(546px, 1fr));
        gap: 41px;
        grid-auto-flow: dense;
        margin-top: 40px;

        @media (max-width: 1024px) {
            grid-template-columns: repeat(auto-fill, minmax(100%, 1fr));
            gap: 20px;
        }

        .chat__item {
            background: #fff;
            padding: 30px 20px;
            border: 2px solid #D2D2D2;

            .justify-content-end {
                @media (max-width: 1024px) {
                    justify-content: flex-start !important;
                }

            }

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


    .mysales {
        margin-top: 33px;

        .add__product {
            margin-bottom: 33px;
            padding: 10px 20px;
            border: 2px solid #828282;
            background: transparent;

            font-size: 16px;
            font-style: normal;
            font-weight: 400;
            line-height: 130%;
            /* 20.8px */
            text-transform: uppercase;
            font-family: var(--int);
            color: #000;
        }

        .salesmob {
            display: none !important;

            @media (max-width: 1024px) {
                display: flex !important;
                flex-direction: column;
                gap: 20px;
            }
        }

        .salespc {
            @media (max-width: 1024px) {
                display: none !important;
            }
        }

        .sale__slider {
            display: flex;
            gap: 15px;

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

                @media (max-width: 1024px) {
                    width: 100% !important;
                    padding: 20px;
                }

                h1 {
                    margin: 20px 0;
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

                span {
                    font-size: 16px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: normal;
                    text-transform: uppercase;
                    font-family: var(--int);
                    color: #000;
                }

                button,
                a {
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

                    @media (max-width: 1024px) {
                        font-size: 12px;
                    }
                }

                .buttons {
                    display: flex;
                    gap: 9px;
                }

                .images {
                    display: flex;
                    gap: 20px;

                    @media (max-width: 1024px) {
                        display: grid;
                        grid-template-columns: repeat(auto-fill, minmax(88px, 1fr));
                        gap: 20px;
                        grid-auto-flow: dense;
                    }

                    img {
                        width: 130px;
                        height: 130px;
                        object-fit: cover;

                        @media (max-width: 1024px) {
                            width: 100%;
                            height: 90px;
                        }
                    }
                }
            }
        }
    }

    .navs {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 30px;


        @media (max-width: 1024px) {
            gap: 20px;
            width: 100%;
            flex-direction: column;
        }

        .activeTab {
            background: #fff;
        }

        div {
            display: flex;
            gap: 30px;

            @media (max-width: 1024px) {
                //  flex-direction: column;
                gap: 20px;
                width: 100%;
            }

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

                @media (max-width: 1024px) {
                    flex: 1;
                    font-size: 12px;
                    white-space: nowrap;
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
        margin: 0 0 30px;

        @media (max-width: 1024px) {
            font-size: 20px;
        }
    }
}
</style>