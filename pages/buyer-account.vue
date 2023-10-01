<template>
    <div class="account">

        <h1>личный кабинет</h1>

        <div class="navs">
            <div>
                <button @click="activeTab = 0" :class="{ activeTab: activeTab == 0 }">История покупок</button>
                <button @click="activeTab = 1" :class="{ activeTab: activeTab == 1 }">транзакции</button>
            </div>
            <div>
                <button @click="activeTab = 3" :class="{ activeTab: activeTab == 3 }">аккаунт</button>
            </div>
        </div>
        <div class="myBuys buysmob" v-if="activeTab == 0">
            <div class="slide" v-for="item in buys" :key="item.order_id">
                <div class="images">
                    <NuxtLink v-for="link in item.items" :to="'/product/' + link.products.id">
                        <img :src="link.products.add_image[0].image" alt="">
                    </NuxtLink>
                </div>

                <h1>ЗАКАЗ №{{ item.order_id }}</h1>
                <span>ДАТА Покупки: {{ formatDate(item.items[0].date) }}</span>
                <h1>{{ item.full_price.toLocaleString() }} ₸</h1>


            </div>
        </div>
        <div class="myBuys buyspc" v-if="activeTab == 0">
            <swiper :slides-per-view="4" :auto-height="true" :space-between="30" :breakpoints="breakpoints"
                :modules="modules" :navigation="navigation2">
                <swiper-slide class="slide" v-for="item in buys" :key="item.order_id">
                    <div class="images">
                        <NuxtLink v-for="link in item.items" :to="'/product/' + link.products.id">
                            <img :src="link.products.add_image[0].image" alt="">
                        </NuxtLink>
                    </div>

                    <h1>ЗАКАЗ №{{ item.order_id }}</h1>
                    <span>ДАТА Покупки: {{ formatDate(item.items[0].date) }}</span>
                    <h1>{{ item.full_price.toLocaleString() }} ₸</h1>
                </swiper-slide>

            </swiper>
            <div class="swipernavs">
                <img src="@/assets/img/prev.svg" class="prev" alt="">
                <img src="@/assets/img/next.svg" class="next" alt="">
            </div>
        </div>

        <div class="acc__info" v-if="activeTab == 3">
            <div class="inp">
                <label for="email">Эл.почта</label>
                <input type="email" v-model="email" placeholder="Эл.почта">
                <!-- <div class="text-right">
                    <button class="save">сохранить изменения</button>
                </div> -->
            </div>
            <div class="inp">
                <label for="password">Пароль</label>
                <input type="password" placeholder="Пароль">
                <div class="text-left">
                    <button @click="logOut()">выйти из аккаунта</button>
                </div>
            </div>
        </div>

        <TheTrans v-if="activeTab == 1" :transactions="transactions"></TheTrans>
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
            email: '',
            activeTab: 0,
            transactions: [],
            chats: [],
            seller: [],
            pathUrl: 'https://merchshop.kz',
            buys: [],
            sendId: null,
            chatId: null,
            myId: null,
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
                321: {
                    slidesPerView: 2,
                    spaceBetween: 30,
                },
                1450: {
                    slidesPerView: 3,
                    spaceBetween: 30,
                }
            },
        }
    },
    methods: {
        formatDate(dateString) {
            const date = new Date(dateString);
            const formattedDate = `${date.getDate().toString().padStart(2, '0')}.${(date.getMonth() + 1).toString().padStart(2, '0')}.${date.getFullYear()}`;
            return formattedDate;
        },
        getAccount() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/buyer/buyer-lk`;
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios
                .get(path)
                .then(response => {
                    this.account = response.data
                    this.myId = response.data.id
                    this.transactions = response.data.transactions
                    this.email = response.data.user.email

                    console.log('Buyer: ', response.data)

                })
                .catch(error => console.log(error));
        },
        openChat(chatId, chatName) {
            this.activeTab = 7;
            this.chatId = chatId;
            this.chatName = chatName
        },
        getBuys() {
            const token = this.getAuthorizationCookie();
            const path = `${this.pathUrl}/api/buyer/buyer-lk/my-purchases`;
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;

            axios
                .get(path)
                .then(response => {
                    const groupedBuys = {};

                    response.data.forEach(item => {
                        const dateKey = item.date;
                        if (!groupedBuys[dateKey]) {
                            groupedBuys[dateKey] = {
                                order_id: null,
                                items: [],
                                full_price: 0,
                                photos: [],
                            };
                        }

                        groupedBuys[dateKey].items.push(item);

                        groupedBuys[dateKey].order_id = item.id;

                        let totalPriceInGroup = 0;

                        groupedBuys[dateKey].items.forEach(groupedItem => {
                            if (
                                typeof groupedItem.products.price === 'number' &&
                                typeof groupedItem.amount === 'number' &&
                                typeof groupedItem.products.discount === 'number'
                            ) {
                                const discountedPrice = groupedItem.products.price * (1 - groupedItem.products.discount / 100);

                                totalPriceInGroup += discountedPrice * groupedItem.amount;
                            }
                        });

                        groupedBuys[dateKey].full_price = totalPriceInGroup;

                        if (item.products.add_image && item.products.add_image.length > 0) {
                            groupedBuys[dateKey].photos.push(item.products.add_image[0].image);
                        }
                    });

                    this.buys = groupedBuys;
                })
                .catch(error => {
                    console.error(error);
                });
        },


        createChat(id, name) {
            const token = this.getAuthorizationCookie()
            const csrf = this.getCSRFToken()
            const path = `${this.pathUrl}/api/messanger/new-chat`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            axios
                .post(path, {
                    buyer: this.myId,
                    seller: id,
                })
                .then(response => {
                    const chatId = response.data.chat_id
                    this.openChat(chatId, name)
                })
                .catch(error => console.log(error))
        },
        getChats() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/messanger/all-chats`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios
                .get(path)
                .then(res => {
                    this.chats = res.data
                })
                .catch(error => console.log(error))
        },

    },
    mounted() {

        const accType = localStorage.getItem('accountType')
        console.log(accType)
        if (accType == 'buyer-account') {
            this.getAccount()
            this.getChats()
            this.getBuys()
        }
        else {
            window.location.href = '/login'
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

    @media (max-width: 1600px) {
        padding: 150px 50px 60px;
    }

    @media (max-width: 1024px) {
        padding: 150px 20px 60px;
    }

    .acc__info {
        display: flex;
        justify-content: center;
        align-items: flex-start;
        gap: 50px;
        margin: 10.417vw 0;

        @media (max-width: 1024px) {
            flex-direction: column;
            justify-content: flex-start;
            align-items: flex-start;
            gap: 20px;
        }

        .save {
            @media (max-width: 1024px) {
                display: none;
            }
        }


        .inp {
            @media (max-width: 1024px) {
                width: 100%;
            }
        }

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

            @media (max-width: 1024px) {
                width: 100%;
            }
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

            @media (max-width: 1024px) {
                margin-top: 20px;
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

    .buysmob {
        display: none !important;

        @media (max-width: 1024px) {
            display: flex !important;
            flex-direction: column;
            gap: 20px !important;
        }
    }

    .buyspc {
        @media (max-width: 1024px) {
            display: none !important;
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

                @media (max-width: 1024px) {
                    font-size: 12px;
                }
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

    .navs {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 30px;

        @media (max-width: 1024px) {
            gap: 20px;
            width: 100%;
        }

        .activeTab {
            background: #fff;
        }

        div {
            display: flex;
            gap: 30px;

            @media (max-width: 1024px) {
                // flex-direction: column;
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