<template>
    <footer>
        <NuxtLink to="/">
            <img src="@/assets/img/footerlogo.svg">
        </NuxtLink>

        <div>
            <NuxtLink to="/#sales">Акции и скидки</NuxtLink>
            <NuxtLink to="/catalog">Каталог</NuxtLink>
            <NuxtLink to="/about">о нас</NuxtLink>
        </div>
        <div>
            <NuxtLink to="/polytics">политика конфиденциальности</NuxtLink>
            <NuxtLink to="/terms">пользовательское соглашениег</NuxtLink>
            <small>2023 © merchshop</small>
        </div>
    </footer>
</template>
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

    div {
        display: flex;
        flex-direction: column;

        gap: 20px;

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
        }
    }
}
</style>