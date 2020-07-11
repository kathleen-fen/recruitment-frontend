 single item component
<template>
<!-- single item component -->
    <div class="item">
        <hr>
        <a :href="item.link" target="_blank"><h3 class="title">{{ item.title }}</h3></a>
        <div>{{ item.pubDate }}</div>
        <img :src="item.media.$.url" alt="img">
        <div class="content" v-html="item.content"></div>
    </div>
</template>
<script>
export default {
    name: 'FeedItem',
    props: {
        item: Object
    }
}
</script>
<style lang="scss" scoped>
img {
    display: block;
    margin: 20px auto;

}
.item {
   margin: 20px;
}   
</style>