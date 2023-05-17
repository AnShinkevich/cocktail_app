<script setup>
import AppLayout from "../components/AppLayout.vue";
import CocktailThumb from "../components/CocktailThumb.vue";
import { useRootStore } from "@/stores/root";
import { storeToRefs } from "pinia";

const rootStore = useRootStore();
rootStore.getIngredients();

const { ingredients, ingredient, cocktails } = storeToRefs(rootStore);

function getCocktails() {
    rootStore.getCocktails(rootStore.ingredient)
}

function removeIngredient() {
    rootStore.setIngredient(null)
}
</script>

<template>
    <AppLayout imgUrl="/src/assets/img/bg-1.jpg" :backFunc="removeIngredient" :is-back-button-visible="!!ingredient">
        <div class="wrapper">
            <div v-if="!ingredient || !cocktails" class="info">
                <div class="title">Choose your drink</div>
                <div class="line"></div>
                <div class="select-wrapper">
                    <el-select
                        v-model="rootStore.ingredient"
                        placeholder="Choose main ingredient"
                        size="large"
                        filterable
                        allow-create
                        class="select"
                        @change="getCocktails"
                    >
                        <el-option
                            v-for="item in ingredients"
                            :key="item.strIngredient1"
                            :label="item.strIngredient1"
                            :value="item.strIngredient1"
                        />
                    </el-select>
                </div>
                <div class="text">
                    Try our delicious cocktail recipes for every occasion. Find delicious cocktail recipes by ingredient through our cocktail generator.
                </div>
                <img src="/src/assets/img/coctails.png" class="img" alt="Coctails">
            </div>
            <div v-else class="info">
                <div class="title">COCKTAILS WITH {{ ingredient}}</div>
                <div class="line"></div>
                <div class="cocktails">
                    <CocktailThumb
                        v-for="cocktail in cocktails"
                        :key="cocktail.idDrink"
                        :cocktail="cocktail"
                    ></CocktailThumb>
                </div>
            </div>
        </div>
    </AppLayout>
</template>

<style lang="scss" scoped>
@import '../assets/styles/main';
.select-wrapper{
    padding-top: 3.125rem;
}
.select{
    width: 13.75rem;
}
.text{
    max-width: 32.25rem;
    margin: 0 auto;
    padding-top: 3.125rem;
    line-height: 225%;
    letter-spacing: 0.1em;
    color: $textMuted;
}
.img{
    margin-top: 3.75rem;
}
.cocktails{
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    max-height: 25rem;
    overflow-y: auto;
    margin-top: 3.75rem;
}
</style>