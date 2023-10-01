<template>
    <div class="catalog">
        <h1 v-if="category == 'catalog'">каталог</h1>
        <div class="category__block" v-else>
            <img src="@/assets/img/catmob1.png" class="catimgmob" alt="">
            <img :src="getImage1(category)" alt="" class="img-fluid catimgpc">
            <h2>{{ getCategoryName(category) }}</h2>
            <h1>{{ getCategoryName(category) }}</h1>
            <img :src="getImage2(category)" alt="" class="img-fluid catimgpc">
            <img src="@/assets/img/catmob2.png" class="catimgmob" alt="">
        </div>

        <div class="sort__body">
            <button @click.stop="toggleSort">
                <span>сортировать</span>
                <img :class="{ opened: sort }" src="@/assets/img/sort.svg" alt="">
            </button>

            <div class="sort__block" :class="{ 'sort--open': sort }" @click="stopPropagation">
                <label class="custom-checkbox">
                    <input type="checkbox">
                    <p class="checkbox-text m-0" @click="selectedSort = 2, sortBy('-price')">цена max</p>
                </label>
                <label class="custom-checkbox">
                    <input type="checkbox">
                    <p class="checkbox-text m-0" @click="selectedSort = 1, sortBy('price')">цена min</p>
                </label>
                <label class="custom-checkbox">
                    <input type="checkbox">
                    <p class="checkbox-text m-0" @click="selectedSort = 3, sortBy('-discount')">Скидки max</p>
                </label>
                <label class="custom-checkbox">
                    <input type="checkbox">
                    <p class="checkbox-text m-0" @click="selectedSort = 4, sortBy('discount')">Скидки min</p>
                </label>

                <div class="price">
                    <h2>цена</h2>

                    <div class="inputs">
                        <input type="number" name="from" id="from" placeholder="от ₸" v-model="minPrice"
                            @input="applyFilters">
                        <img src="@/assets/img/line.svg" alt="">
                        <input type="number" name="to" id="to" placeholder="до ₸" v-model="maxPrice" @input="applyFilters">
                    </div>
                </div>
            </div>
        </div>

        <div class="catalog__body">
            <NuxtLink class="catalog__block" v-for="item in catalog.results" :key="item.id" :to="'/product/' + item.id">
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

        <div class="text-right showmore">
            <button ref="showmore" @click="loadMoreProducts()">показать еще</button>
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
            sort: false,
            selectedSort: 0,
            catalog: [],
            minPrice: null,
            maxPrice: null,
            pathUrl: 'https://merchshop.kz',

        }
    },
    methods: {
        getCatalog() {
            const queryParams = new URLSearchParams(window.location.search);
            const categoryParam = queryParams.get('category');



            let url = `${this.pathUrl}/api/products/all-product`;
            if (categoryParam) {
                url = `${this.pathUrl}/api/products/category-product/${categoryParam}`;
            }

            axios
                .get(url)
                .then(response => {
                    this.catalog = response.data;
                })
                .catch(error => {
                    console.error(error);
                });
        },
        loadMoreProducts() {
            if (this.catalog.next) {
                this.$refs.showmore.innerHTML = 'Загружаем'
                axios
                    .get(this.catalog.next)
                    .then(response => {
                        this.$refs.showmore.innerHTML = 'Показать еще'
                        this.catalog.results.push(...response.data.results);
                        this.catalog.next = response.data.next;
                    })
                    .catch(error => {
                        console.error(error);
                    });
            }
            else {
                this.$refs.showmore.innerHTML = 'Больше ничего нет (;'
            }
        },
        sortBy(ordering) {
            this.sort = false
            const queryParams = new URLSearchParams(window.location.search);
            const categoryParam = queryParams.get('category');



            let path = `${this.pathUrl}/api/products/all-product?ordering=${ordering}`;
            if (categoryParam) {
                path = `${this.pathUrl}/api/products/category-product/${categoryParam}?ordering=${ordering}`;
            }
            axios
                .get(path)
                .then(response => {
                    this.catalog = response.data;

                })
                .catch(error => {
                    console.error(error);
                });
        },

        applyFilters() {
            const params = new URLSearchParams();
            if (this.minPrice !== null) {
                params.append('price__gte', this.minPrice);
            }
            if (this.maxPrice !== null) {
                params.append('price__lte', this.maxPrice);
            }
            this.fetchFilteredProducts(params);
        },
        fetchFilteredProducts(params) {
            const queryParams = new URLSearchParams(window.location.search);
            const categoryParam = queryParams.get('category');



            let path = `${this.pathUrl}/api/products/all-product?${params.toString()}`;
            if (categoryParam) {
                path = `${this.pathUrl}/api/products/category-product/${categoryParam}?${params.toString()}`;
            }
            axios
                .get(path)
                .then(response => {
                    this.catalog = response.data;
                })
                .catch(error => {
                    console.error(error);
                });
        },
        toggleSort() {
            this.sort = !this.sort;
            if (this.sort) {
                document.addEventListener('click', this.closeSort);
            } else {
                document.removeEventListener('click', this.closeSort);
            }
        },
        closeSort() {
            this.sort = false;
            document.removeEventListener('click', this.closeSort);
        },
        stopPropagation(event) {
            event.stopPropagation();
        },
        getImage1(category) {
            const imageMap = {
                8: '/img/office1.png',
                9: '/img/kids1.png',
                1: '/img/stickers1.png',
                2: '/img/cloth1.png',
                3: '/img/cases1.png',
                4: '/img/posters1.png',
                5: '/img/households1.png',
                7: '/img/pets1.png',
                6: '/img/accessories1.png',
                10: '/img/gits1.png'
            };
            return imageMap[category] || '';
        },
        getImage2(category) {
            const imageMap = {
                8: '/img/office2.png',
                9: '/img/kids2.png',
                1: '/img/stickers2.png',
                2: '/img/cloth2.png',
                3: '/img/cases2.png',
                4: '/img/posters2.png',
                5: '/img/households2.png',
                7: '/img/pets2.png',
                6: '/img/accessories2.png',
                10: '/img/gits2.png'
            };
            return imageMap[category] || '';
        },
        getCategoryName(category) {
            const categoryNameMap = {
                8: 'КАНЦЕЛЯРИЯ',
                9: 'Для Детей',
                1: 'Стикеры',
                2: 'Одежда',
                3: 'Чехлы на\nтелефон',
                4: 'Постеры',
                5: 'Товары для дома',
                7: 'ДЛЯ ПИТОМЦЕВ',
                6: 'Аксессуары',
                10: 'Подарочные наборы'
            };
            return categoryNameMap[category] || '';
        },
    },
    computed: {
        category() {

            return this.$route.query.category || 'catalog';
        },
    },
    mounted() {

        this.getCatalog()

    }
}
</script>
<script setup>

useSeoMeta({
    title: 'Каталог | MerchShop',
    ogTitle: 'Каталог | MerchShop',
    description: 'Каталог | MerchShop',
    ogDescription: 'Каталог | MerchShop',
})
</script>
<style lang="scss" scoped>
.catalog {
    padding: 150px 100px 60px;

    @media (max-width: 1600px) {
        padding: 150px 50px 60px;
    }

    @media (max-width: 1024px) {
        padding: 100px 20px 60px;
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

    .catalog__body {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(257px, 1fr));
        gap: 35px;
        grid-auto-flow: dense;

        @media (max-width: 1024px) {
            gap: 20px;
            grid-template-columns: repeat(auto-fill, minmax(165px, 1fr));
        }

        .catalog__block {
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

    .sort__body {
        position: relative;
        width: 100%;
        margin: 30px 0;

        .sort--open {
            transform: scale(1) !important;
        }

        .sort__block {
            position: absolute;
            left: 0;
            top: 100%;
            transition: all .3s ease;
            transform: scale(0);

            background: #fff;
            padding: 20px;
            margin-top: 30px;

            .price {
                h2 {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 600;
                    line-height: normal;
                    text-transform: uppercase;
                    font-family: var(--int);
                    color: #000;
                    margin-bottom: 20px;
                }

                .inputs {
                    display: flex;
                    align-items: center;
                    gap: 4px;

                    input {
                        border-radius: 5px;
                        border: 2px solid #000;
                        text-align: right;
                        padding: 9px 10px;
                        width: 100px;
                        height: 35px;

                        font-size: 14px;
                        font-style: normal;
                        font-weight: 400;
                        line-height: normal;
                        text-transform: uppercase;
                        font-family: var(--int);
                        color: #000;
                    }
                }
            }

            label {
                display: block;
            }
        }

        .opened {
            transform: rotate(90deg) !important;
        }


        button {
            display: flex;
            align-items: center;
            gap: 10px;

            padding: 10px 20px;
            border: 1px solid #D2D2D2;
            background: #fff;

            font-size: 20px;
            font-style: normal;
            font-weight: 400;
            line-height: normal;
            text-transform: uppercase;
            font-family: var(--int);
            color: #000;

            img {
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
    }

    .category__block {
        white-space: pre-line;
        position: relative;
        opacity: 0.8;
        border-radius: 20px;
        // background: url('@/assets/img/tex.svg'), lightgray 0% 0% / 40.00000059604645px 40.00000059604645px repeat;
        background-color: #F7BFCA;
        padding: 25px 9.427vw 54px;

        display: flex;
        justify-content: space-between;

        @media (max-width: 1024px) {
            padding: 34px 17px 34px 33px;
        }

        .catimgpc {
            @media (max-width: 1024px) {
                display: none;
            }
        }

        .catimgmob {
            display: none;

            @media (max-width: 1024px) {
                display: block;
                margin-top: 0 !important;
            }
        }

        img {
            &:last-child {
                margin-top: 25px;
            }
        }

        h1,
        h2 {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
            width: 100%;

            font-size: 57.6px;
            font-style: normal;
            line-height: 130%;
            font-family: var(--pr);
            text-transform: uppercase;
        }

        h1 {
            color: #fff;
            font-weight: 400;
            top: 44%;

            @media (max-width:1024px) {
                font-size: 20px;
                top: 46%;
            }
        }

        h2 {
            color: #000;
            top: 44.5%;
            font-weight: 600;

            @media (max-width:1024px) {
                font-size: 20px;
                top: 46.5%;
            }
        }
    }
}

.custom-checkbox p {
    font-family: var(--int);
    font-size: 16px;
    font-style: normal;
    font-weight: 400;
    line-height: 130%;
    color: #000;
    white-space: nowrap;
    text-transform: uppercase;
}

.custom-checkbox input[type="checkbox"] {
    opacity: 0;
    position: absolute;
    border-radius: 3px;
}

.custom-checkbox .checkbox-text:before {
    content: '';
    display: inline-block;
    vertical-align: middle;
    width: 20px;
    height: 20px;
    margin-right: 10px;
    border: 2px solid #000;
    border-radius: 3px;
    margin-bottom: 3px;
}

.custom-checkbox input[type="checkbox"]:checked+.checkbox-text:before {
    content: url('@/assets/img/check.svg');
    font-size: 16px;
    color: black;
    text-align: center;
    line-height: 20px;
    background: transparent;
}

.custom-checkbox {
    margin-bottom: 22px;

}

.custom-checkbox:last-child {
    margin-bottom: 0 !important;

    @media (max-width: 1024px) {
        margin-bottom: 22px !important;
    }
}
</style>
