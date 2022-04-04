<template>
    <ul class="news__list">
        <div v-for="article in articles" class="news__item">
            <img :src=article.urlToImage width = "200" height = "200" />
            <p >{{ article.title }} </p>
            <p> {{ article.description }} </p>
        </div>
    </ul>
</template>

<script>
export default {
    data() {
        return {
            articles: []
        };
    },
    created() {
        let self = this;
        fetch('https://newsapi.org/v2/top-headlines?country=us',
    {
        headers: {
            'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
        }
    })
    .then(function(response) {
        return response.json();
    })
    .then(function(data) {
        console.log(data);
        self.articles = data.articles
    });
    }
};
</script>
<style>
.news__list{
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 50px;
    
}
.news__item{
    border-bottom: solid blue;
}

</style>