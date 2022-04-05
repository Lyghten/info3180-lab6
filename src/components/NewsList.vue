<template>
	<ul class="news__list">
			<li v-for="article in articles" class="news__item">{{article.title}} 
			<img class="images" :src = "article.urlToImage"/>
			{{article.description}}</li>
			
			<form @submit.prevent="searchNews" class="d-flex flexcolumn justify-content-center">
                </form>
		                                                   
	</ul>
</template>


<script>
export default {
	data() {
	  return {
	      articles: []
	      searchTerm:''
	  }
     },
     created() {
     	   let self= this;
           fetch('https://newsapi.org/v2/top-headlines?country=us',
         {
      headers: {
          'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
      }
  })
           .then(function(response){
             return response.json();
           })
           .then(function(data) {
             console.log(data);
             self.articles= data.articles;
           });
        }           
           
     };
     
</script>