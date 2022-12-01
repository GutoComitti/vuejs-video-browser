<template>
  <div class="container">
    <SearchBar @termChange="onTermChange"></SearchBar>
    <div class="row">
      <VideoDetail :video="selectedVideo"></VideoDetail>
      <VideoList :videos="videos" @videoSelect="onVideoSelect"></VideoList>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from "./components/SearchBar";
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';

// Google API documentation: https://developers.google.com/youtube/v3/docs/search
const API_KEY = 'AIzaSyDR0SPom8u7YGlMSNSW7sT2ngpDJ4hTiJc';
const YOUTUBE_API_SEARCH_ENDPOINT = 'https://www.googleapis.com/youtube/v3/search';

export default {
  name: "App",
  data() {
    return {
      videos: [],
      selectedVideo: null
    }
  },
  components: {
    SearchBar,
    VideoList,
    VideoDetail
  },
  methods: {
    onTermChange(term) {
      axios.get(YOUTUBE_API_SEARCH_ENDPOINT, {
        params: {
          key: API_KEY,
          type: 'video',
          part: 'snippet',
          q: term
        }
      }).then(this.handleYoutubeResponse);
    },
    handleYoutubeResponse(res) {
      this.videos = res.data.items;
      console.log(this.videos);
    },
    onVideoSelect(video){
      this.selectedVideo = video;
    }
  }
};
</script>

<style>
</style>