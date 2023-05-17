<template>
    <input class="input-styling"
     placeholder="Search your state" 
     type="text"
     :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)">
</template>
<script >
export default{
    props: ['modelValue'],
    emits: ['update:modelValue'],
}
</script>
<style lang="scss">
@use '@/assets/global-mixins.scss';
.input-styling{
    @include global-mixins.clamp(13rem, 100%, 60rem, 4rem, 100%, 4rem, #23395B,);
    @include global-mixins.fontStyling(200, #F0F7F4, 20px);
    border-radius: 5px;
    border: none;
    text-align: center;
  }
.input-styling:focus{
    outline: #F0F7F4;
}
</style>