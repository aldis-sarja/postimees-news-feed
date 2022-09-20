<template>
    <div>
        <Article v-for="article in news" v-bind:key="article"
        :article="article" />
    </div>
</template>

<script>
import axios from 'axios';
import Article from './Article';


export default {
  components: { Article },
    name: 'NewsTab',
    data() {
        return {
            news: []
        }
    },
    async created() {
        const payload = {
            headers: {
                'Accept': 'application/json'
            }
        }

        try {
            const res = await axios.get(
            'https://services.postimees.ee/rest/v1/sections/81/editorsChoice/articles?limit=5',
            payload
            );

            for(const item of res.data) {
                const article = {id: item.id};
                const slug = null;
                if (item.slug) {
                    slug = item.slug;
                } else if (item.audioarticles[0].slug) {
                   slug = item.audioarticles[0].slug.replace("/^\d+\-/", "");
                }
                article.url = "https://www.postimees.ee/" + article.id + "/" + slug;
                article.title = item.headline;
                const dateTime = new Date(item.datePublished);
                article.date = dateTime.toLocaleDateString();
                if (item.media[0].thumbnail) {
                    article.urlImg = item.media[0].thumbnail.sources.square.xsmall;
                } else if (item.media[0].sources) {
                    article.urlImg = item.media[0].sources.square.xsmall;
                }

                const description = null;
                if (item.articleLead.html) {
                 description = item.articleLead.html;
                } else if (item.articleLead[0].html) {
                    description = item.articleLead[0].html;
                }
                article.description = description.replace(/<\/?p>/g, "");

                this.news.push(article);
                article = null;
            }
        } catch (error) {
            console.log(error)
        }
        
    },
}
</script>
