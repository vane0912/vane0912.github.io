<template>
  <div class="input-button">
    <div class="wrap-in-li">
      <input class="input-styling" v-model="userCity" @input="getValue" type="text" >
      <div v-if="this.userCity.length > 0" ref="toggleDisplay" class="allCities">
        <ul style="list-style-type: none; padding: 0;" ref="dontDisplay" @click="selectDiv($event)">
          <li v-for="cities in citiesApi">
            {{ cities }}</li>
        </ul>
      </div>
    </div>
    <button @click="searchCountry" class="button-styling">Search</button>
  </div>
</template>
<script >
export default{
  data(){
    return{
      citiesApi:[],
      userCity: ''
    }
  },
  watch:{
    userCity(txt){
      if(txt.length > 0){
        fetch('https://countriesnow.space/api/v0.1/countries')
        .then(response => response.json()).then(data => data.data).then(value => {
          const toLc = value.map(values => values.cities).flat(1).sort()
          const userCity = toLc.filter(values => values.toLowerCase().startsWith(this.userCity.toLowerCase()))
          const emptyArray = ['No city found']
          userCity.length === 0 ? this.citiesApi = emptyArray : this.citiesApi = userCity;
        })
      }
    }
  },
  methods:{
    selectDiv(click){
      const div = this.$refs.toggleDisplay
      div.classList.toggle("display-none");
      this.userCity = click.target.textContent;
    },
    searchCountry(){
      this.$router.push(`/about/${this.userCity}`);
    }
  }
}
</script>
<style lang="scss">
@use '@/assets/global-mixins.scss';
.input-styling{
    @include global-mixins.minMax(100%, 60rem, 97%, 10rem);
    @include global-mixins.fontStyling(200, #F0F7F4, 20px);
    border-radius: 2px;
    border: none;
    text-align: center;
}
.input-styling:focus{
    outline: #23395B 2px;
}
.wrap-in-li{
  @include global-mixins.heightAndWidth(100%, 100%, transparent)
}
.filter{
    display: flex;
    flex-direction: column;
    @include global-mixins.heightAndWidth(100%, 100%, transparent)
}
.button-styling{
    @include global-mixins.minMax(60%, 20rem, 100%, 10rem, #70ABAF);
    @include global-mixins.fontStyling(100, #F0F7F4, 20px);
    border-radius: 5px;
    border: solid 1px #23395B;
    position: relative;
    right: 1%;
    cursor: pointer;
}
.input-button{
    @include global-mixins.minMax(100%, 100%, 100%, 4rem, transparent);
    @include global-mixins.positionDisplay(flex-start, row, center);
} 
.allCities{
  @include global-mixins.fontStyling(100, #F0F7F4, 20px);
  @include global-mixins.heightAndWidth(auto, 100%, #23395B);
  z-index: 1;
  max-height: 10rem;
  border-radius: 2px;
  overflow: scroll;
}
.allCities li{
  cursor: pointer;
  padding: 2%;
  &:hover{
    background-color: #2a456c;
  }
}
.display-none{
  display: none;
}
</style>