<template>
    <div class="catalog">
        <h1 v-if="category == 'catalog'">каталог</h1>
        <div class="category__block" v-else>
            <img :src="getImage1(category)" alt="" class="img-fluid">
            <h2>{{ getCategoryName(category) }}</h2>
            <h1>{{ getCategoryName(category) }}</h1>
            <img :src="getImage2(category)" alt="" class="img-fluid">
        </div>

        <div class="sort__body">
            <button @click.stop="toggleSort">
                <span>сортировать</span>
                <img :class="{ opened: sort }" src="@/assets/img/sort.svg" alt="">
            </button>

            <div class="sort__block" :class="{ 'sort--open': sort }" @click="stopPropagation">
                <label class="custom-checkbox">
                    <input type="checkbox">
                    <p class="checkbox-text m-0">цена max</p>
                </label>
                <label class="custom-checkbox">
                    <input type="checkbox">
                    <p class="checkbox-text m-0">цена min</p>
                </label>
                <label class="custom-checkbox">
                    <input type="checkbox">
                    <p class="checkbox-text m-0">популярное</p>
                </label>
                <label class="custom-checkbox">
                    <input type="checkbox">
                    <p class="checkbox-text m-0">Скидки</p>
                </label>

                <div class="price">
                    <h2>цена</h2>

                    <div class="inputs">
                        <input type="number" name="from" id="from" placeholder="от ₸">
                        <img src="@/assets/img/line.svg" alt="">
                        <input type="number" name="to" id="to" placeholder="до ₸">
                    </div>
                </div>
            </div>
        </div>

        <div class="catalog__body">
            <NuxtLink to="/catalog" class="catalog__block">
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
            <NuxtLink to="/catalog" class="catalog__block">
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
            <NuxtLink to="/catalog" class="catalog__block">
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
            <NuxtLink to="/catalog" class="catalog__block">
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
            <NuxtLink to="/catalog" class="catalog__block">
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
            <NuxtLink to="/catalog" class="catalog__block">
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
            <NuxtLink to="/catalog" class="catalog__block">
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
            <NuxtLink to="/catalog" class="catalog__block">
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
            <NuxtLink to="/catalog" class="catalog__block">
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
            <NuxtLink to="/catalog" class="catalog__block">
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
            <NuxtLink to="/catalog" class="catalog__block">
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
            <NuxtLink to="/catalog" class="catalog__block">
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
</template>
<script>
export default {
    data() {
        return {
            sort: false,
        }
    },
    methods: {
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
                office: '/img/office1.png',
                kids: '/img/kids1.png',
                stickers: '/img/stickers1.png',
                cloth: '/img/cloth1.png',
                cases: '/img/cases1.png',
                posters: '/img/posters1.png',
                households: '/img/households1.png',
                pets: '/img/pets1.png',
                accessories: '/img/accessories1.png',
                gifts: '/img/gits1.png'
            };
            return imageMap[category] || '';
        },
        getImage2(category) {
            const imageMap = {
                office: '/img/office2.png',
                kids: '/img/kids2.png',
                stickers: '/img/stickers2.png',
                cloth: '/img/cloth2.png',
                cases: '/img/cases2.png',
                posters: '/img/posters2.png',
                households: '/img/households2.png',
                pets: '/img/pets2.png',
                accessories: '/img/accessories2.png',
                gifts: '/img/gits2.png'
            };
            return imageMap[category] || '';
        },
        getCategoryName(category) {
            const categoryNameMap = {
                office: 'КАНЦЕЛЯРИЯ',
                kids: 'Для Детей',
                stickers: 'Стикеры',
                cloth: 'Одежда',
                cases: 'Чехлы на\nтелефон',
                posters: 'Постеры',
                households: 'Товары для дома',
                pets: 'ДЛЯ ПИТОМЦЕВ',
                accessories: 'Аксессуары',
                gifts: 'Подарочные наборы'
            };
            return categoryNameMap[category] || '';
        },
    },
    computed: {
        category() {

            return this.$route.query.category || 'catalog';
        },
    },
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

        .catalog__block {
            background: #fff;
            text-decoration: none;
            border: 1px solid #D2D2D2;
            padding: 10px;
            display: flex;
            flex-direction: column;
            max-width: 340px;

            img {
                width: 100%;
                height: 214px;
                object-fit: cover;

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
                    }
                }

                p {
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
        background: url('@/assets/img/tex.svg'), lightgray 0% 0% / 40.00000059604645px 40.00000059604645px repeat;
        background-color: #F7BFCA;
        padding: 25px 9.427vw 54px;

        display: flex;
        justify-content: space-between;

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
        }

        h2 {
            color: #000;
            top: 44.5%;
            font-weight: 600;
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
