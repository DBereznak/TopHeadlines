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
            newsOption: 'General',
            options: ['general', 'entertainment',  'health', 'science', 'sports', 'technology'],
        };
    },
    methods: {
        getNewsOption(option) {
            console.log(option);
            this.newsOption = option;
        }
    }
}
</script>

<style scoped lang="scss">
.navbar-fixed{ 
    margin-bottom: 50px;
}
</style>