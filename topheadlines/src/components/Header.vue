<template>
<div>
    <ul>
        <li v-for="(option, index) in options" :key="index">
            <button v-on:click="getNewsOption(option)">{{option}}</button>
        </li>
    </ul>
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
            newsOption: 'test',
            options: ['entertainment', 'general', 'health', 'science', 'sports', 'technology'],
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


</style>