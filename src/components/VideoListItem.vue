<template>
    <li class="list-group-item media" @click="onVideoSelect">
        <img :src="thumbnail.url" class="mr-3">
        <div class="media-body">
            {{ video.snippet.title }}
        </div>
    </li>
</template>
<script>
export default {
    name: 'VideoListItem',
    props: ['video'],
    computed: {
        thumbnail(){
            return this.video.snippet.thumbnails.default;
        }
    },
    methods: {
        onVideoSelect: function() {
            this.$emit('videoSelect', this.video);
        }
    }

}

</script>

<style scoped>
    li {
        display: flex;
        cursor: pointer;
    }

    li:hover {
        background-color: #eee;
    }
</style>