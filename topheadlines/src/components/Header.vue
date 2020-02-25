<template>
<div>
<div class="navbar-fixed ">
    <nav>
    <div class="nav-wrapper purple darken-3">

        <span class="right time">{{ updateTime | moment("dddd, MMMM Do YYYY") }}</span>
    <ul class="left hide-on-med-and-down">
        <li v-for="(option, index) in options" :key="index">
            <a v-on:click="getNewsOption(option)">{{option.toUpperCase()}}</a>
        </li>
        <li>
            <a v-on:click="getWeather()">WEATHER</a>
        </li>
        <li>
    <li class="search">
    <form>
        <div class="input-field">
          <input id="search" type="search" v-model="customSearch" required>
          <label class="label-icon" for="search"><i class="material-icons">search</i></label>
          <i class="material-icons">close</i>
          
        </div>
        <button v-on:click="getCustomSearch(customSearch)">search</button>
      </form>
        </li>

    </ul>
    </div>
    </nav>
</div>
    <div v-if="!showWeather">
    <News :optionID="newsOption" />
    </div>
    <Weather v-else />
</div>
</template>
<script>
import News from './News.vue';
import Weather from './Weather'

export default {
    components: {
        News,
        Weather
    },
    data() {
        return {
            customSearch: '',
            showWeather: false,
            newsOption: 'general',
            options: ['general', 'entertainment',  'health', 'science', 'sports', 'technology'],
             currentDate: Date(),
        };
       
    },
    methods: {
        getNewsOption(option) {
            this.showWeather = false;
            this.newsOption = 'country=us&category=' + option;
        },
        
        getCustomSearch(customSearch){
            this.showWeather = false;
            this.newsOption = 'q='+ customSearch;
        },
        getWeather(){
            this.showWeather = true;
        }

    }, computed: {
        updateTime: function() {
            return Date.now();
        }
    }
}
</script>

<style scoped lang="scss">
.navbar-fixed{ 
    margin-bottom: 50px;
    ul{
        padding-left: 50px;
    }
    form{
        position:absolute;
    .input-field{
        width: 300px;
    }
    input[type=search]{
        color: #6a1b9a;
        font-size: 24px;
    }
    button{
        display: none;
        opacity: 0;
        position: absolute;
        top: -200px;
    }
    }
    .time{
        font-size: 16px;
        font-weight: 600;
        padding-right: 50px;
    }
}
</style>