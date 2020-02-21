<template>
<div>
<div class="navbar-fixed ">
    <nav>
    <div class="nav-wrapper purple darken-3">

        <a href="#" class="brand-logo right">Logo</a>
    <ul class="left hide-on-med-and-down">
        <li v-for="(option, index) in options" :key="index">
            <a href="#" v-on:click="getNewsOption(option)">{{option.toUpperCase()}}</a>
        </li>
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
    <News :optionID="newsOption" />
</div>
</template>
<script>
import News from './News.vue'
export default {
    components: {
        News
    },
    data() {
        return {
            customSearch: '',
            newsOption: 'general',
            options: ['general', 'entertainment',  'health', 'science', 'sports', 'technology'],
        };
    },
    methods: {
        getNewsOption(option) {

            this.newsOption = 'country=us&category=' + option;
        },
        
        getCustomSearch(customSearch){
            this.newsOption = 'q='+ customSearch;
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

}
</style>