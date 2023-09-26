<template>
    <div class="seller">
        <PrevPage></PrevPage>
        <h1>SHOPCASE</h1>

        <div class="seller__info">
            <img src="@/assets/img/seller.png" alt="">

            <div class="seller__desc">
                <h2>Описание:</h2>

                <div v-html="description"></div>
            </div>
        </div>

        <div class="seller__products">
            <h1>товары продавца</h1>

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
</template>
<script>
export default {
    data() {
        return {
            description: 'Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание'
        }
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

            .similar__block {
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