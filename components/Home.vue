<template>
  <div class="container mx-auto px-8 text-center">
        <div class="bg fixed top-0 left-0 w-full h-full"></div>
        <div class="flex items-center justify-center mx-auto">
            <h1 class="text-6xl text-white">
                Search artists:
            </h1>
        </div>
        <input class="border p-3 rounded-md mt-4 text-xl mb-4 focus:outline-none focus:ring focus:border-red-300 focus:border-2 focus:border-blue-400" placeholder="Enter artist's name ==>" type="text" v-model="query" @keypress.enter="search">
        <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-4">
            <a class="h-full" :href="item.artistViewUrl" v-for="(item, index) in searchResults.results" :key="index">
                <div class="group card h-full cursor-pointer relative rounded-xl bg-gray-200 p-2">
                    <img class="w-full h-40 rounded-xl" :src="item.artworkUrl100" alt="Artists img">
                    <div class="icon opacity-0 group-hover:opacity-100 absolute top-32 right-4 translate-y-2 rounded-full p-2 bg-green-600 inline-block">
                        <svg class="icon__svg" height="16" role="img" width="16" viewBox="0 0 24 24" aria-hidden="true"><polygon points="21.57 12 5.98 3 5.98 21 21.57 12" fill="white"></polygon></svg>
                    </div>
                    <h3 class="card__title text-2xl">{{item.artistName}}</h3>
                    <p class="card__text">{{item.collectionCensoredName}}</p>
                </div>
            </a>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    data(){
        return{
            query: '',
            url_base: `https://itunes.apple.com/search?term=`,
            searchResults: {
                results: [

                ]
            }
        };
    },
    methods: {
    search() {
      axios
        .get(`${this.url_base}${this.query}&entity=musicVideo`)
        .then((response) => {
          this.searchResults = response.data;
          console.log(this.searchResults);
        })
        .catch((e) => {
          console.log(e);
        });
    },
    },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Dongle:wght@300;400;700&family=Lobster&display=swap');
body{
    font-family: Lobster;
}
.bg{
    background-color: rgb(83, 83, 83);
    background-image: linear-gradient(rgba(0,0,0,.6) 0,#121212 100%),var(--background-noise);
    background-repeat: no-repeat;
    z-index: -1;
}
/* .icon{
    top: 8rem;
} */
.card:hover .icon__svg{
    animation: infiniteRotate 2s linear infinite;
}
@keyframes infiniteRotate {  
    0% { -webkit-transform: rotate(0deg); }
    100% { -webkit-transform: rotate(360deg); }
}
</style>