<template>
    <header ref="addAnimation" class="align-header">
        <div>
           <img src="./assets/icon-weather.png">
        </div>
        <div class="header-text">
           <h1 class="white-letters">Search your city here</h1>
           <inputComponent/>
           <button @click="showAnimation()" class="button-styling">Search</button>
        </div>
    </header>
</template>

<script>
  import inputComponent from '@/components/input-component.vue'
  export default{
    components: {inputComponent},
    methods:{
      showAnimation(){
        this.$refs.addAnimation.classList.add("header-animation")
      }
    }
  }
</script>

<style lang="scss">
  @use "@/assets/global-mixins.scss";
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap');
  body{
    margin: 0;
    font-family: 'Roboto', sans-serif;
  }
  header{
    width: 100vw;
    height: 100vh;
    background-color: #1282A2;
  }
  .align-header{
    display: flex;
    justify-content: space-evenly;
    align-items: center;
  }
  .white-letters{
    color: #FEFCFB;
    font-weight: 300;
  }
  .header-animation{
    animation-name: reduce-header;
    animation-fill-mode: forwards;
    animation-duration: 3s;
  }
  .button-styling{
    cursor: pointer;
    @include global-mixins.inputAndButtonStyles;
  }
  @keyframes reduce-header{
    from{ height: 100vh;}
    to{height: 50vh;}
  }
</style>
