<template>
    <input class="input-styling" type="text">
</template>
<style lang="scss">
@use "@/assets/global-mixins.scss";
    .input-styling{
        width: 75%;
        @include global-mixins.inputAndButtonStyles;
    }
</style>