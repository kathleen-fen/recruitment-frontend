<template>
    <div class="item">
        <h2 class="title">{{ item.title }}</h2>
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