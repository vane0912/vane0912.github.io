<template>
    <button class="button-styling">Search</button>
</template>
<style lang="scss">
@use '@/assets/global-mixins.scss';
 .button-styling{
     @include global-mixins.heightAndWidth(80%, 30%, #70ABAF);
     @include global-mixins.fontStyling(100, #F0F7F4, 20px);
     border-radius: 5px;
     border: solid 1px #23395B;
     cursor: pointer;
   }
</style>
