<template>
<div>
      <h1>{{ stripQuery(optionID.toUpperCase()) || 'GENERAL' }}</h1>
      <h2 v-if="noArticles">Your Query returned no articles</h2>
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
          <a class="purple-text text-darken-3" :href="article.url" target="_blank">Click to full article</a>
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
  props: {  
  optionID: {
    type: String
  }},
  data() {
    return {
      noArticles: false,
      newsData: [],
      API_KEY: config.API_KEY
    };
  },
  methods: {
    getNews(option) {
      axios
        .get(
          `https://newsapi.org/v2/top-headlines?${option}&sortBy=popularity&pageSize=50&apiKey=${this.API_KEY}`
        )
        .then(response => {
          if(response.data.articles.length > 0){
          this.newsData = response.data.articles;
            this.noArticles = false;
          } else{
            this.noArticles = true;
            this.newsData = [];
          }
        })
        .catch(error => {
          console.error(error);
        });
    },
    stripQuery(id){
      let title = (id === undefined) ? 'GENERAL' : id.split('=');
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
h1, h2{
  text-align: center;
}
.news-reel{
  display: flex;
  flex-flow: row wrap;
  .card{
    width: 350px;
    height: auto;
    margin: 20px;
    .card-image{
      img{
        max-height: 350px;
      }
    }
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
    .card-action{
      a{
        color: #6a1b9a;
        &:hover{
          text-decoration: underline;
        }
      }
    }
  }
}
</style>
