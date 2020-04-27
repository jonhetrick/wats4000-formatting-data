<template>
  <div class="results">
    <h1>
      Top Movies from the 20
      <sup>th</sup> Century
    </h1>
    <p class="search-meta">
      <span class="current-page">
        <b>Current Page:</b>
        {{ page }}
      </span>

      <span class="total-pages">
        <b>Pages:</b>
        {{ total_pages }}
      </span>

      <span class="total-results">
        <b>Count:</b>
        {{ results.length }}
      </span>
    </p>

    <ul>
      <li v-for="movie in results" class="movie-item" :key="movie.id">
        <img
          v-bind:src="'https://image.tmdb.org/t/p/w150_and_h225_bestv2' + movie.poster_path"
          v-bind:alt="movie.title + 'Poster'"
          class="poster-image"
        />

        <h2 class="title">
          <a v-bind:href="'https://www.themoviedb.org/movie/' + movie.id">{{movie.title}}</a>
        </h2>
        <div class="ratings">
          <span v-if="movie.vote_average > 8" class="rating-category critics-choice">Critic's Choice</span>

          <span
            v-else-if="movie.vote_average === 7 || 8"
            class="rating-category well-liked"
          >Well Liked</span>

          <span v-else-if="movie.vote_average < 7" class="rating-category stinker">Stinker</span>

          <span class="vote-average">{{movie.vote_average}}</span> with
          <span class="vote-count">{{movie.vote_count}}</span> votes
        </div>
        <p class="overview">{{ movie.overview }}</p>
        <p class="release-date">Original Release: {{movie.release_date}}</p>
        <ul class="genre-list">
          <li v-for="genre in movie.genres" :key="genre">{{ genre }}</li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>
import apiresults from "../assets/apiresults.js";
export default {
  data() {
    return apiresults;
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  margin: 0 0 1rem 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
.search-meta {
  text-align: right;
}
.movie-item {
  margin: 10px 0;
  padding: 2rem;
  box-shadow: 4px 4px 10px rgba(0, 0, 0, 0.2);
}
.movie-item img {
  float: left;
  margin-right: 1rem;
}
.release-date {
  font-weight: 600;
  font-size: 12px;
  color: #333;
}
.rating-category {
  font-size: 12px;
  color: #fff;
  font-weight: 800;
  background: #ccc;
  padding: 0.5rem;
  border-radius: 4px;
}
.rating-category.critics-choice {
  background: goldenrod;
}
.rating-category.well-liked {
  background: green;
}
.rating-category.stinker {
  background: brown;
}
.genre-list li {
  border-radius: 4px;
  background: #666;
  color: #fff;
  font-weight: 800;
  font-size: 12px;
  padding: 0.5rem;
  display: inline-block;
  margin-right: 10px;
}
a {
  color: #42b983;
}
</style>