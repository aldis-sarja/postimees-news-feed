<template>
    <div class="article">
        <a :href="article.url" target="_blank">
            <img class="image-link"
             :src="article.urlImg"  alt="No Image"
             />
        </a>
        <div class="text-section">
            <a  class="a-link"
             :href="article.url" target="_blank">
                <h2>{{ article.title }}</h2>
            </a>
        <div class="description-section">
            <p>{{ article.description }}</p>
            <p>&bull; {{ article.date }}</p>
        </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Article',
    props: ['article']
};
</script>


<style>
.article {
    display: flex;
    flex-direction: row;
    padding: 5px;
    margin: 2px;
    border: 1px solid rgb(145, 173, 204)
}

.text-section {
    display: flex;
    flex-direction: column;
    margin: 0 10px;
}

.description-section {
    display: flex;
    flex-direction: column;
    padding: 0;
    margin: 0 10px;
}

body {
  background-color: lightslategray;
}

.a-link:hover {
  color: whitesmoke;
  background-image: linear-gradient(to right, lightslategray, #494757);
}

.image-link:hover {
    box-shadow: black 0 5px 15px;
}
</style>