<template>
<div>
      <h1>{{ stripQuery(optionID.toUpperCase()) }}</h1>
  <div class="news-reel">
    <div class="row news-card" v-for="(article, index) in newsData" :key="index">
      <div class="col s12 m7">
      <div class="card">
        <div class="card-image">
          <img :src="article.urlToImage" />
        </div>
        <div class="card-content">
          <h4>{{article.title}}</h4>
          <ul>
            <li>{{article.source.name}}</li>
            <li>{{article.author}}</li>
          </ul>
             <p v-if="article.content">{{article.content}}</p>
        </div>
        <div class="card-action">
          <a :href="article.url" target="_blank">Click to full article</a>
        </div>     
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
          `https://newsapi.org/v2/top-headlines?${option}&apiKey=${this.API_KEY}`
        )
        .then(response => {
          this.newsData = response.data.articles;
          console.log(response.data.articles);
        })
        .catch(error => {
          console.error(error);
        });
    },
    stripQuery(id){
      let title = (id === undefined) ? 'GENERAL' : id.split('=');
      console.log(title)
      return title[2];
    }
  },
  watch:{
    optionID: function() {
      this.getNews(this.optionID)
    }
  },

  created() {
    this.getNews('country=us&category=general');
  }
};
</script>

<style lang="scss">
h1{
  text-align: center;
}
.news-reel{
  display: flex;
  flex-flow: row wrap;
  .card{
    width: 350px;
    height: auto;
    margin: 20px;
    .card-content{
      h4{
        font-size: 1rem;
        font-weight: bold;
      }
      ul{
        text-align: left;
        li{
          color: #5b5b5b;
        }
      }
      p{
        font-size: 14px;
      }
    }
  }
}
</style>
