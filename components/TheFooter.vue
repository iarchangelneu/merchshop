<template>
    <footer v-if="!hideFooterOnPages.includes($route.name)">
        <NuxtLink to="/">
            <img src="@/assets/img/footerlogo.svg">
        </NuxtLink>

        <div class="trap">
            <NuxtLink to="/#sales">Акции и скидки</NuxtLink>
            <NuxtLink to="/catalog">Каталог</NuxtLink>
            <NuxtLink to="/about">о нас</NuxtLink>
        </div>
        <div class="netrap">
            <NuxtLink to="/polytics">политика конфиденциальности</NuxtLink>
            <NuxtLink to="/terms">пользовательское соглашение</NuxtLink>
            <small>2023 © merchshop</small>
        </div>
    </footer>
</template>
<script>
export default {
    data() {
        return {
            hideFooterOnPages: ['login', 'register'],
        }
    }
}
</script>
<style lang="scss">
footer {
    display: flex;
    gap: 100px;
    align-items: flex-start;
    margin: 0 100px;
    padding: 40px 60px 80px;
    border-radius: 20px 20px 0px 0px;
    border-top: 2px solid #D2D2D2;
    border-right: 2px solid #D2D2D2;
    border-left: 2px solid #D2D2D2;


    @media (max-width: 1600px) {
        margin: 0 50px;
        padding: 40px 30px 60px;
        gap: 30px;
    }

    @media (max-width: 1024px) {
        margin: 0 20px;
        padding: 20px 30px 25px;
        flex-direction: column;
        gap: 20px;
    }

    div {
        display: flex;
        flex-direction: column;

        gap: 20px;

        &:last-child {
            a {
                @media (max-width: 1024px) {
                    font-size: 14px;
                }
            }
        }

        a {
            font-size: 20px;
            font-style: normal;
            font-weight: 500;
            line-height: normal;
            text-transform: uppercase;
            font-family: var(--int);
            color: #000 !important;
            text-decoration: none !important;

        }

        small {
            font-size: 16px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            /* 20.8px */
            text-transform: uppercase;
            font-family: var(--int);
            color: #828282;

            @media (max-width: 1024px) {
                font-size: 14px;
            }
        }
    }
}
</style>