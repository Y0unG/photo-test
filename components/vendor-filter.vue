<template>
    <div class="vendor-filter"> 
        <div class="vendor-filter__header">
            <div class="vendor-filter__title">
                Фильтр:
                <span class="vendor-filter__name">По альбомам</span>
                <span class="vendor-filter__name">Избранное</span>
            </div>
        </div>
        <div class="vendor-filter__scroll-wrap">
            <div class="vendor-filter__scroll">
                <div class="vendor-filter__list" id="list">
                    <div class="vendor-filter__item" v-for="photo in photos" :key="photo.id">
                        <div>
                            <img :src="`${photo.thumbnailUrl}`" alt="">
                            <p class="vendor-filter__title">{{photos.title}}</p>   
                        </div>
                        <div>
                            <button class="vendor-filter__btn" v-if="isFav" v-on:click="isFav=false">X</button>
                            <button class="vendor-filter__btn" v-if="!isFav" v-on:click="isFav=true">♥</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
    </div>
</template>


<script>
export default {
    name: "list",

    props: {
       isShow: true,
       isFav: false 
    },

    data () {
        return {
            photos: [],
            titles: []
        };
    },

    computed: {},

    async created () {
       const res = await fetch('http://jsonplaceholder.typicode.com/photos?_limit=22');
       const photos = await res.json();
       this.photos = photos;
       const titles = photos.map(({title}) => title.split(" ").shift());
       for (let i=0; i<titles.length; i++) {
           photos.title=titles[i];
       }
        
    },

    methods: {},
};
</script>

<style lang="scss">
.vendor-filter {
    font-weight: 700;
    font-family: Open Sans, Roboto, sans-serif;
    width: 1300px;
    height: 600px;
    margin: auto;
    padding: 3.6rem 4.8rem 6rem;
    font-size: 1.2rem;
    background: #ffffff;
    border-radius: 1.2rem;
    box-sizing: border-box;
    position: relative;

    &__header {
        margin: 0 0 1.5rem;
    }

    &__title {
        font-weight: bold;
        font-size: 1.4rem;
        line-height: 1.9rem;
    }

    &__name {
        margin: 0 0.5rem;
        text-decoration: underline;
        cursor: pointer;
    }

    &__scroll-wrap {
        overflow: hidden;
    }

    &__scroll {
        width: 100%;
        max-height: 66rem;
        overflow-y: auto;
    }

    &__list {
        position: relative;
        display: flex;
        flex-direction: column;
        flex-wrap: wrap;
        justify-content: flex-start;
        max-height: 500px;
        overflow-y: scroll;
        
    }

    &__item {
        background: #F7F8F9;
        border-radius: 8px;
        padding: 4px;
        margin: 4px;
        display: flex;
        justify-content: space-between;
        width: 260px;
        & div {
            display: flex;
            align-items: center;
        }
        & img {
            max-width: 32px;
            display: inline-block;
        }
        & p {
            margin-left: 11px;
            text-align: left;
            display: inline-block;
        }
        & button {
            border: none;
            outline: none;
            background: none;
            color: red;
            font-size: 24px;
            cursor: pointer;
        }
    }
}
</style>
