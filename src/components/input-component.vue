<template>
    <input class="input-styling" placeholder="Search your country" type="text">
</template>
<style lang="scss">
@use '@/assets/global-mixins.scss';
.input-styling{
    @include global-mixins.heightAndWidth(80%, 60%, #23395B);
    @include global-mixins.fontStyling(200, #F0F7F4, 20px);
    padding: 0px 15px;
    border-radius: 5px;
    border: none;
    text-align: center;
  }
.input-styling:focus{
    outline: #F0F7F4;
}
</style>