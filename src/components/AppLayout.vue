<script setup>
import {
   Back,
} from '@element-plus/icons-vue'

const props = defineProps({
    imgUrl: {
        type: String,
        required: true,
    },
    backFunc: {
        type: Function,
        required: true,
    },
    isBackButtonVisible: {
        type: Boolean,
        default: true,
    }
})
</script>

<template>
    <div class="root">
        <div :style="`background-image: url(${imgUrl})`" class="img"></div>
        <div class="main">
            <div class="btns">
                <el-button
                    v-if="isBackButtonVisible"
                    type="success"
                    :icon="Back"
                    circle
                    class="back"
                    @click="backFunc"
                />
                <el-button class="btn" >Get random cocktail</el-button>
            </div>
            <slot></slot>
        </div>
    </div>
</template>


<style lang="scss" scoped>
@import "../assets/styles/main";

.root{
    display: flex;
    min-height: 100vh;
    background-color: $background;
}
.img{
    width: 50%;
    background-repeat: no-repeat;
    background-position: 50% 50%;
    background-size: cover;
}
.main{
    position: relative;
    width: 50%;
    padding: 2rem 2.5rem;
}
.btn{
    position: absolute;
    top: 2rem;
    right: 2.5rem;
    font-size: 1rem;
    font-family: 'Raleway', 'Arial', sans-serif;
    background-color: $accent;
    border-color: $accent;
    color: $text;
    &:hover,&:active{
        background-color: darken($accent, 10%);
        border-color: darken($accent, 10%);
    }
}
.btns{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.back{
    background-color: transparent;
    border-color: #fff;
    &:hover{
        border-color: $accent;
    }
}
</style>