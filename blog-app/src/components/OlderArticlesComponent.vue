<template>
    <section class="older-posts section">
        <div class="container">
            <h2 class="title section-title" data-name="Artigos mais antigos">Artigos mais antigos</h2>
            <div class="older-posts-grid-wrapper d-grid">
                <a v-for="(article, index) in olderArticle" 
                    :article="article" 
                    :key="article.id" 
                    :index="index" 
                    :href="'./article/' + article.id" 
                    class="article d-grid"
                >
                    <div class="older-posts-article-image-wrapper">
                        <img :src="article.image" alt="" class="article-image">
                    </div>
                    <div class="article-data-container">
                        <div class="article-data">
                            <span>{{ article.data }}</span>
                            <span class="article-data-spacer"></span>
                            <span>{{ article.time_read }}</span>            
                        </div>
                        <h3 class="title article-title">{{ article.title }}</h3>
                        <i class="fas fa-light fa-eye" style="font-size: 1.5rem;">
                            <span> {{ Math.floor(Math.random() * 500) }}</span>
                        </i>
                        <i class="fas fa-thumbs-up" style="font-size: 1.5rem;padding-left:3%;">
                            <span> {{ Math.floor(Math.random() * 30) }}</span>
                        </i>
                    </div>
                    <span class="article-category">{{ article.category.name }}</span>
                    </a>
            </div>
            <div class="see-more-container">
                <a href="./artigos.html" class="btn see-more-btn place-items-center">
                    Veja mais
                    <i class="ri-arrow-right-s-line"></i>
                </a>
            </div>
        </div>
    </section> 
</template>

<script setup>
    import { onMounted, ref } from "vue";
    import { allArticles } from "../http/blog-api";
    // import OlderArticle from "./articles/OlderArticle.vue";
    
    const olderArticle = ref([]);

    onMounted(async () => {
        const response = await allArticles();
        const articles = response.data.data;

        const olderArticlesList = articles.slice(0, Math.min(articles.length, 10));
        olderArticlesList.sort(() => Math.random() - 0.5);

        const randomArticles = olderArticlesList.slice(0, 6);
        olderArticle.value = randomArticles;
    });
</script>