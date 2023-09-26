<template>
    <div class="about">
        <h1>о нас</h1>
        <div class="about__body">
            <img src="@/assets/img/aboutas.png" alt="">

            <div class="about__desc">
                <p>Добро пожаловать в наш уникальный маркетплейс для подарков и удовольствия! Мы рады приветствовать
                    вас в мире удивительных подарков и товаров, которые принесут радость как вам, так и вашим близким.</p>

                <p><span>Кто мы?</span> Мы — команда энтузиастов, которые собрались вместе, чтобы создать место, где каждый
                    сможет найти идеальный подарок для любого случая или просто порадовать себя чем‑то особенным. Нашей
                    целью является объединение уникальных продавцов и покупателей в одном месте, чтобы сделать процесс
                    поиска и выбора подарков увлекательным и приятным.</p>

                <p><span>Что мы предлагаем?</span> Наши полки наполнены разнообразными сокровищами: от оригинальных подарков
                    и украшений ручной работы до эксклюзивных товаров и стильных аксессуаров. У нас есть что‑то для каждого,
                    независимо от их вкусов и интересов. Мы гордимся тем, что предоставляем доступ к товарам, которые
                    вы могли бы найти только у нас.</p>

                <p><span>Почему выбирать именно нас?</span> Мы стремимся к выдающемуся качеству, инновационному дизайну
                    и безупречному обслуживанию клиентов. Наша команда усердно работает над тем, чтобы каждый заказ
                    был осуществлён с любовью и заботой, чтобы подарок оставил незабываемое впечатление.</p>
                <p>С нами каждый шаг — ваши эмоции важны! Мы понимаем, что подарки и покупки — это не просто транзакции,
                    но и способ выразить свою заботу и любовь. Мы верим, что важно оставаться верными этому принципу,
                    поэтому гарантируем вам приятный и незабываемый опыт покупок с нами.</p>
                <p>Спасибо, что выбрали нас. Мы гордимся тем, что можем помочь вам делать жизнь ярче и уникальнее, один
                    подарок за другим. Добро пожаловать в наш магазин — вашему новому источнику вдохновения для подарков
                    и собственных радостей!</p>


                <div class="register">
                    <NuxtLink to="/register">регистрация</NuxtLink>
                    <img src="@/assets/img/about.svg" alt="">
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {

        }
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'О Нас | MerchShop',
    ogTitle: 'О Нас | MerchShop',
    description: 'О Нас | MerchShop',
    ogDescription: 'О Нас | MerchShop',
})
</script>
<style lang="scss" scoped>
.about {
    padding: 150px 100px 82px;

    .about__body {
        display: flex;
        gap: 142px;
        align-items: flex-start;

        .about__desc {
            max-width: 925px;

            .register {
                margin-top: 30px;
                display: flex;
                justify-content: space-between;
                align-items: center;

                a {
                    text-decoration: none;
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
                }
            }

            p {
                margin-bottom: 10px;
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                color: #000;

                span {
                    font-weight: 600;
                }

                &:last-child {
                    margin-bottom: 0;
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
        margin-bottom: 30px;
    }
}
</style>