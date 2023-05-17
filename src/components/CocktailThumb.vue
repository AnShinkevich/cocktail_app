<script setup>
const props = defineProps({
    cocktail: {
        type: Object,
        required: true,
    }
})
</script>

<template>
    <div class="root">
        <RouterLink :to="`/cocktails/${cocktail.idDrink}`">
            <div
                :style="`background-image: url(${cocktail.strDrinkThumb})`"
                class="pic"
            ></div>
            <div class="name">{{cocktail.strDrink}}</div>
        </RouterLink>
    </div>
</template>

<style lang="scss" scoped>
@import "../assets/styles/main";
.root{
    width: calc((100% - 4.75rem)/3);
    margin-right: 2.375rem;
    padding-bottom: 1.25rem;
    &:nth-child(3n+3){
        margin-right: 0;
    }
}
.pic{
    width: 7.5rem;
    height: 7.5rem;
    margin: 0 auto;
    background-repeat: no-repeat;
    background-position: 50% 50%;
    background-size: 100%;
}
.name{
    width: 100%;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    padding-top: 0.9375rem;
    letter-spacing: 0.1em;
}
</style>