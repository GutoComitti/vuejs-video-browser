<template>
  <div class="container">
    <SearchBar @termChange="onTermChange"></SearchBar>
    <VideoList :videos="videos"></VideoList>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from "./components/SearchBar";
import VideoList from './components/VideoList';

// Google API documentation: https://developers.google.com/youtube/v3/docs/search
const API_KEY = 'AIzaSyDR0SPom8u7YGlMSNSW7sT2ngpDJ4hTiJc';
const YOUTUBE_API_SEARCH_ENDPOINT = 'https://www.googleapis.com/youtube/v3/search';

export default {
  name: "App",
  data() {
    return {
      videos: []
    }
  },
  components: {
    SearchBar,
    VideoList
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
    }
  }
};
</script>

<style>
</style>