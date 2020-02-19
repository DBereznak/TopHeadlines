<template>
  <div>
    <h1>{{ optionID.toUpperCase() }}</h1>
    <div class="row" v-for="(article, index) in newsData" :key="index">
      <div class="col s12 m7">
      <div class="card">
        <div class="card-image">
          <img :src="article.urlToImage" />
          <h4>{{article.title}}</h4>
        </div>
        <div class="card-content">
             <p>{{article.content}}</p>
        </div>
        <div class="card-action">
          <a :href="article.url">Click to full article</a>
        </div>     
      </div>
      </div> 
    </div>
  </div>
</template>

<script>
import axios from "axios";
import config from "../config/config"

export default {
  props: ["optionID"],
  data() {
    return {
      newsData: [],
      API_KEY: config.API_KEY
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
