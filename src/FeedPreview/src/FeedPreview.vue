<template>
    <div>
        <div v-if="!loading">
            <!-- head -->
            <nav class="navbar navbar-dark bg-primary fixed-top">
                <div class="navbar-brand" href="#">{{ feed.title }}</div>
                <form class="form-inline my-2 my-lg-0">
                    <input class="form-control mr-sm-2" type="search" placeholder="Search by title" aria-label="Search" v-model="search">
                </form>
            </nav>
            <!-- feed -->
            <div class="container">
                <h1>{{ feed.description }}</h1>
                <div>{{ feed.lastBuildDate }}</div>
                <div class="row" >
                    <!-- feed items -->
                    <div class="col-12" v-for="i in filteredFeed" :key="i.index">
                        <FeedItem :item="i" />
                    </div>
                </div>
            </div>
        </div>
        <!-- while it is loading -->
        <div class="loader"  v-if="loading"><Loader /></div>
        <!-- if there is an error -->
        <div v-if="err" class="error"><Error v-on:tryAgain="tryAgain()"/></div>
    </div>
</template>
<script>

import Parser from './../../../node_modules/rss-parser/dist/rss-parser'
import FeedItem from './FeedItem'
import Loader from './Loader'
import Error from './Error'

export default {
    components: {
        FeedItem,
        Loader,
        Error
    },
    data () {
        return {
            feed: {},
            err: null,
            loading: true,
            search: null
        }
    },
    props: {
        url: String
    },
    created() {
        this.feedRequest();
    },
    computed: {
        //for searching
        filteredFeed() {
            return this.search ? this.feed.items.filter(el => el.title.toLowerCase().includes(this.search.trim().toLowerCase())) :  this.feed.items
        }
    },
    methods: {
        //request of feed
        async feedRequest() {
            const CORS_PROXY = "https://cors-anywhere.herokuapp.com/"
            let parser = new Parser({
                customFields: {
                feed: ['lastBuildDate', 'language'],
                item: ['description',['media:content','media']],
                }
            });
            try {
                this.feed = await parser.parseURL(CORS_PROXY+this.url)
                this.loading = false
                this.err = null
            } catch(e) {
                this.err = e
                this.loading = false
            }
        },
        // if there id an error we can try again
        tryAgain() {
            this.loading = true
            this.err = null
            this.feedRequest()
        }
    } 
} 
</script>
<style lang="scss" scoped>
h1 {
    text-align: center;
    margin-top: 70px;
    margin-bottom: 20px;
}
.loader {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>