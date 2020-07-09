/* eslint-disable no-console */
/* eslint-disable no-console */
<template>
    <div>
        <div v-for="i in feed.items" :key="i.index"><FeedItem :item="i" /></div>
    </div>
</template>
<script>

import Parser from './../../../node_modules/rss-parser/dist/rss-parser'
import FeedItem from './FeedItem'

export default {
    components: {
        FeedItem
    },
    data () {
        return {
            feed: {},
            err: false,
            loading: true
        }
    },
    props: {
        url: String
    },
    async created() {
        const CORS_PROXY = "https://cors-anywhere.herokuapp.com/"
        let parser = new Parser({
            customFields: {
            feed: ['lastBuildDate', 'language'],
            item: ['description',['media:content','media']],
            }
        });
        this.feed = await parser.parseURL(CORS_PROXY+this.url)
        // eslint-disable-next-line no-console
        console.log(this.feed);
        
       /*  feed.items.forEach(item => {
            // eslint-disable-next-line no-console
            console.log(item.title + ':' + item.link)
            // eslint-disable-next-line no-console
            console.log('description:' + item.description)
            // eslint-disable-next-line no-console
            console.log(item.media)
        }); */
  } 
} 
</script>