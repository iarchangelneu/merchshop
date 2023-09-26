<template>
    <div class="page">
        <div class="text-center">
            <h1>ВЫВОД СРЕДСТВ ПРОШЕЛ УСПЕШНО</h1>

            <NuxtLink to="/">На главную</NuxtLink>
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
    title: 'Баланс успешно пополнен | MerchShop',
    ogTitle: 'Баланс успешно пополнен | MerchShop',
    description: 'Баланс успешно пополнен | MerchShop',
    ogDescription: 'Баланс успешно пополнен | MerchShop',
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

    }

    a {
        padding: 10px 20px;
        border: 1px solid #D2D2D2;
        display: inline-block;
        margin-top: 30px;
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