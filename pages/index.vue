<template>

    <div class="iframe">
      
          <input class="textR" type="text" v-model="searchInput">
          <button class="button" style="vertical-align:middle" @click="search(searchInput)" ><span>  Search</span></button>
    
      <div v-if="videos!=null" id="iframeContainer" style="display: inline-table;">
                <iframe class="overall" v-for="item in videos" :key="item.id.videoId" width="640" height="480" 
        :src="'https://www.youtube.com/embed/'+item.id.videoId" 
        frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
        allowfullscreen></iframe>
      </div>

  </div>

</template>

<script>

  export default {
    created() {
      let axios = require('axios');

        let params = {
        part: 'snippet',
        key: 'AIzaSyBKyJnMiM1wWdNTwftiPkpkqUjfuFLglVU',
        q: 'كايروكى',
        maxResults: 5,
        type: 'video'
                    };
    var parent = this;
     axios.get('https://www.googleapis.com/youtube/v3/search', { params })
    .then(response => {
    parent.videos = response.data.items }
    )
    .catch(error => console.error(error));
    },   
    mounted(){
      setTimeout(function(){     let count = document.getElementById("iframeContainer").children;
        if (count.length%2 != 0) {count[count.length -1].style.cssText = "margin: auto; display: table-cell;"};
},1000)
    },
    data() {
      return {
        videos: null,
        loading: true,
        searchInput: ""
      }
    },
    methods: {
      search(keyword){
        
             let axios = require('axios');

        let params = {
        part: 'snippet',
        key: 'AIzaSyBqJ9T8tven3Ge0_hNDWKjJ3lqOoL5N90s',
        q: keyword,
        maxResults: 5,
        type: 'video'
                    };
    var parent = this;
     axios.get('https://www.googleapis.com/youtube/v3/search', { params })
    .then(response => {
    parent.videos = response.data.items }
    )
    .catch(error => console.error(error));
      },
    }
  }

</script>
<style>

body {background-color: black;}
input[type=text] {
  background-color: white;
  background-image: url('../components/searchicon.png');
    background-position: -1px 0px;
    background-repeat: no-repeat;
    padding-left: 30px;
    background-size: 14%;
    color : rgb(0, 0, 0);
}
.overall{
    padding: 23px 20px;
    background-color: #272727;
    margin: 40px 50px;
    border: 1px red solid;
}
.iframe {
    padding: 23px 20px;
    margin: 40px 100px;
}
.button {
  display: inline-block;
  border-radius: 4px;
  background-color: #f4511e;
  border: none;
  color: #FFFFFF;
  text-align: center;
  font-size: 28px;
  padding: 20px;
  width: 200px;
  transition: all 0.5s;
  cursor: pointer;
  margin: 5px;
}
.textR{
      padding: 5px 5px;
    margin: 20px 50px;

}
.button span {
  cursor: pointer;
  display: inline-block;
  position: relative;
  transition: 0.5s;
}

.button span:after {
  content: '\00bb';
  position: absolute;
  opacity: 0;
  top: 0;
  right: -20px;
  transition: 0.5s;
}

.button:hover span {
  padding-right: 25px;
}

.button:hover span:after {
  opacity: 1;
  right: 0;
}
</style>