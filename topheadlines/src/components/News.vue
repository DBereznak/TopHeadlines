<template>
  <div>
    <h1>{{ optionID }}</h1>
    <ul>
        <li v-for="(article, index) in newsData" :key="index">
            <img :src="article.urlToImage" width="500px" height="auto" />
            <h4>{{article.title}}</h4>
            <a :href="article.url">Click to full article</a>
            <p>{{article.content}}</p>
        </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import dotenv from 'dotenv'

dotenv.config();

export default {
  props: ["optionID"],
  data() {
    return {
      newsData: [],
      API_KEY: 'cb2ecc4d780c4eceabc7795d21eaf11b'
    };
  },
  methods: {
    getNews(option) {
      axios
        .get(
          `https://newsapi.org/v2/top-headlines?country=us&category=${option}&apiKey=${this.API_KEY}`
        )
        .then(response => {
          this.newsData = response.data.articles;
          console.log(response.data.articles);
        })
        .catch(error => {
          console.error(error);
        });
    }
  },
  watch:{
    optionID: function() {
      this.getNews(this.optionID)
    }
  },

  created() {
    this.getNews('general');
  }
};
</script>

<style lang="scss"></style>
