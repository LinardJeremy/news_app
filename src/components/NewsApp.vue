<template>
  <div>
    <header>
      <h1>News App</h1>

      <select  @change="fetchData()" v-model="selected">
        <option value="kr">Corée du Sud</option>
        <option value="us">Etats-Unis</option>
        <option :selected="true" value="be">Belgique</option>
        <option value="jp">Japon</option>
        <option value="au">Australie</option>
        <option value="gb">Grande-Bretagne</option>
        <option value="fr">France</option>
      </select>
    </header>
    <section class="cardNew" v-for="(actu, index) in articles" :key="index">
      <div class="divTitleAndImg">
        <h2 class="titleNew">{{ actu.title }}</h2>
        <span class="source">Source : {{ actu.source.name}}</span>
        
        <img v-if="actu.urlToImage != null" class="imgNew" :src="actu.urlToImage" />
        <p class="sorryNoImage" v-if="actu.urlToImage === null">Désolé nous ne possédons pas d'image d'illustration pour cet article ! </p>
        <a target="_blank" :href="actu.url"><button class="seeArticle"> Voir l'article</button> </a>
      </div>
      <div class="divDescription">
        <p v-if="actu.description !=null">{{actu.description}}</p>
        <p v-if="actu.description ===null">Désolé il n'existe pas de texte de description pour cet article</p>

      </div>
      </section>
  </div>
</template>

<script>

import axios from "axios";
export default {
  name: "NewsApp",
  data() {
    return {
      news: null,
      articles: null,
      selected: "be",
      ApiUrl:
        "http://newsapi.org/v2/top-headlines?country=kr&apiKey=6b596994f2e44facb2a780c35d55a7d4",
    };
  },
  methods: {
    ApirLinkComputed: function() {

     this.ApiUrl = ("http://newsapi.org/v2/top-headlines?country=" + this.selected +"&apiKey=6b596994f2e44facb2a780c35d55a7d4");
     return this.ApiUrl
    },
    fetchData: function() {
     this.ApiUrl = ("http://newsapi.org/v2/top-headlines?country=" + this.selected +"&apiKey=6b596994f2e44facb2a780c35d55a7d4");
      this.articles = [];
      axios.get(this.ApiUrl).then((reponse) => {
        this.news = reponse;
        this.articles = reponse.data.articles;
      });
    }
  },
  mounted() {
    this.fetchData();
  },
};
 
</script>

<style>
header{
  background-color: rgb(52, 49, 240);
  top:0;
  height: 150px;
  text-align: center;
}
header h1{
  color: white;
  margin-top: 0;
}
.imgNew{
  width: 350px;
  height: 250px;
  display: block;
  margin-right: auto;
}
.cardNew{
  display: flex;
  justify-content: space-between;
  width: 80%;
  border: solid black 1px;
  border-radius: 5px;
  background-color: rgb(253, 244, 244);
  margin: auto;
  margin-top: 25px;
  height: 500px;
}
.divTitleAndImg{
  width: 50%;
}
.titleNew{
  text-align: left;
  margin-right: auto;
  width: 100%;
  font-size: 24px;
  color: black;

}
.source{
  display: block;
  margin-bottom: 10px;
  width: 100%;
  margin-right: auto;
}
.seeArticle{
  display: block;
  margin-top: 10px;
  margin-bottom: 10px;
  margin-right: auto;
  width: 100px;
  padding: 5px;
  background-color: rgb(13, 112, 224);
  color: white;
}
.sorryNoImage{
  width: 40%;
  text-align: center;
  margin-right: auto;
  margin-left: auto;
  font-weight: bold;
}
.divDescription{
  width: 45%;
  height: 150px;
  margin-top:auto;
  margin-bottom: auto;
}
.divDescription p{
  text-align: center;
  line-height: 180%;
  
}
</style>
