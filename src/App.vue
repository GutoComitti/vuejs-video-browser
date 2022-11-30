<template>
  <div id="app">
    <SearchBar @termChange="onTermChange"></SearchBar>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from "./components/SearchBar";
// https://developers.google.com/youtube/v3/docs/search
const API_KEY = 'AIzaSyDR0SPom8u7YGlMSNSW7sT2ngpDJ4hTiJc';
const YOUTUBE_API_SEARCH_ENDPOINT = 'https://www.googleapis.com/youtube/v3/search';

export default {
  name: "App",
  components: {
    SearchBar,
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
      console.log(res);
    }
  }
};
</script>

<style>
</style>