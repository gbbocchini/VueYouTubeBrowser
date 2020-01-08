<template>
  <div class="container">
      <SearchBar @termChange="onTermChange"></SearchBar>
      <div class="row">
      <VideoDetail :video="selectedVideo"></VideoDetail>
      <VideoList :videos="videosList" @videoSelect="onVideoSelect"></VideoList>
      </div>
  </div>
</template>


<script>
import SearchBar from "@/components/SearchBar";
import VideoList from "@/components/VideoList";
import VideoDetail from "@/components/VideoDetail";
const API_KEY =
import axios from 'axios'

export default {
    name: 'App',
    components: {
        SearchBar,
        VideoList,
        VideoDetail,
    },

    data: function() {
        return { videosList: [], selectedVideo:null }

    },
    methods: {
        onVideoSelect(video){
          this.selectedVideo = video;
        },

        onTermChange(searchTerm){
            axios.get('https://www.googleapis.com/youtube/v3/search',{
                params:{
                    key: API_KEY,
                    type: 'video',
                    part: 'snippet',
                    q:searchTerm
                }
            }).then(response => {
                this.videosList = response.data.items
            }).catch((e)=>{
                // eslint-disable-next-line no-console
                console.log(e.message)
            })
}
}
}
</script>


<style>
</style>
