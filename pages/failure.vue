<template>
    <div class="page">
        <div class="text-center">
            <h1>Ошибка транзакции</h1>

            <NuxtLink to="/refill">ПОВТОРИТЬ ПОПЫТКУ</NuxtLink>
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
            pathUrl: 'https://merchshop.kz',
        }
    },
    methods: {
        sendRequest(reference) {
            const token = this.getAuthorizationCookie();
            const path = `${this.pathUrl}/api/money/failure/${reference}`;
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios
                .get(path)
                .then(response => {
                    console.log(response)
                    if (response.status == 200) {
                        //  window.location.href = '/'
                    }
                })
                .catch(error => {
                    console.log(error);
                });
        },
    },
    mounted() {
        const url = window.location.href;
        const match = url.match(/order_pay_merchshop_(\d+)/);

        if (match) {
            this.extractedValue = match[0];
            console.log(this.extractedValue);

            this.sendRequest(match[0])
        }
    },
}
</script>
<script setup>
useSeoMeta({
    title: 'Ошибка транзакции | MerchShop',
    ogTitle: 'Ошибка транзакции | MerchShop',
    description: 'Ошибка транзакции | MerchShop',
    ogDescription: 'Ошибка транзакции | MerchShop',
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