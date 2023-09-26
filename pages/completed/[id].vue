<template>
    <div class="page">
        <div class="text-center">
            <h1>вАШ ЗАКАЗ УСПЕШНО ОФОРМЛЕН! информация о товаре отправлена на вашу почту</h1>
            <h2>номер заказа: 540291</h2>

            <NuxtLink to="/catalog">продолжить покупки</NuxtLink>
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
    title: 'Заказ успешно оформлен | MerchShop',
    ogTitle: 'Заказ успешно оформлен | MerchShop',
    description: 'Заказ успешно оформлен | MerchShop',
    ogDescription: 'Заказ успешно оформлен | MerchShop',
})
</script>
<style lang="scss" scoped>
.page {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;

    h1,
    h2 {
        font-size: 20px;
        font-style: normal;
        font-weight: 400;
        line-height: 130%;
        /* 26px */
        text-transform: uppercase;
        font-family: var(--int);
        color: #000;
        margin-bottom: 20px;

        &:last-child {
            margin-bottom: 0;
        }
    }

    a {
        padding: 10px 20px;
        border: 1px solid #D2D2D2;
        display: inline-block;
        margin-top: 50px;
        text-decoration: none;

        font-size: 16px;
        font-style: normal;
        font-weight: 500;
        line-height: normal;
        text-transform: uppercase;
        font-family: var(--int);
        color: #000;
    }
}
</style>