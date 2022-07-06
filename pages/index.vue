<template>
  <div class="home">
    <MainNav />
    <Hero />
    <!-- Search -->
    <div class="container search">
      <input
        v-model.lazy="searchInput"
        placeholder="Seach"
        @keyup.enter="$fetch"
      />
      <button
        v-show="searchInput !== ''"
        class="search__btn"
        @click="clearSearch"
      >
        Clear Search
      </button>
    </div>
    <!-- Movies -->
    <h1 class="container">Danh sách đang phát</h1>
    <div v-if="searchInput === ''" class="container movie__container">
      <div v-for="(movie, idx) in movies" :key="idx" class="movie__item">
        <div class="movie__card">
          <div class="movie__content">
            <img
              :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
              alt=""
              class="movie__img"
            />
            <span class="movie__point">
              {{ movie.vote_average }}
            </span>
          </div>
          <div class="movie__bg"></div>

          <span class="movie__title">
            {{ movie.title }}
          </span>
          <div class="get-more">
            <NuxtLink
              class="button button-light"
              :to="{ name: 'movies-movieid', params: { id: movie.id } }"
            >
              Get More Info
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>
    <div v-if="searchInput !== ''" class="container movie__container">
      <div
        v-for="(movie, idx) in searchedMovies"
        :key="idx"
        class="movie__item"
      >
        <div class="movie__card">
          <div class="movie__content">
            <img
              :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
              alt=""
              class="movie__img"
            />
            <span class="movie__point">
              {{ movie.vote_average }}
            </span>
          </div>
          <div class="movie__bg"></div>

          <span class="movie__title">
            {{ movie.title }}
          </span>
          <div class="get-more">
            <NuxtLink
              class="button button-light"
              :to="{ name: 'movies-movieid', params: { id: movie.id } }"
            >
              Get More Info
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'IndexPage',
  data() {
    return {
      movies: [],
      searchedMovies: [],
      searchInput: ''
    }
  },
  async fetch() {
    if (this.searchInput === '') {
      await this.getMovies()
      return
    }
    if (this.searchInput !== '') {
      console.log('here')
      await this.searchMovies()
    }
  },

  methods: {
    clearSearch() {
      this.searchInput = ''
    },
    async getMovies() {
      const res = await axios.get(
        `https://api.themoviedb.org/3/movie/now_playing?api_key=6162ae2b1b2025ea6787ef8e689c4b74&language=en-US&page=1`
      )
      console.log(res.data.results)
      res.data.results.forEach((mov) => {
        this.movies.push(mov)
      })
    },
    async searchMovies() {
      console.log(this.searchInput)
      const res = await axios.get(
        `https://api.themoviedb.org/3/search/movie?api_key=6162ae2b1b2025ea6787ef8e689c4b74&language=en-US&page=1&query=${this.searchInput}`
      )
      console.log(res.data.results)
      res.data.results.forEach((mov) => {
        this.searchedMovies.push(mov)
      })
    }
  }
}
</script>

<style lang="scss" scoped>
h1 {
  margin-top: 4rem;
  font-size: 2.2rem;
}
.home {
  color: #fe843d;
  background: #080d26;
  padding-bottom: 8rem;
}
.movie {
  &__container {
    flex-wrap: wrap;
    display: flex;
  }
  &__type {
    font-weight: 700;
    font-size: 2.2rem;
  }
  &__item {
    width: calc(19% - 13px);
    margin: 20px 13px;
  }
  &__card {
    width: 100%;
    position: relative;
    cursor: pointer;
  }
  &__content {
    position: relative;
  }
  &__img {
    width: 100%;
    height: 350px;
    border-radius: 15px;
  }
  &__point {
    position: absolute;
    bottom: 1rem;
    right: 1rem;
    font-weight: 600;
    font-size: 1.2rem;
    width: 34px;
    height: 44px;
    border-radius: 0.6rem;
    background: #080d26;
    color: #fe843d;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  &__title {
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 3rem;
    font-size: 1.2rem;
    font-weight: 400;
  }
}
.search {
  margin-top: 4rem;
  &__btn {
    padding: 0.8rem 1.4rem;
    border-radius: 0;
  }
}
.get-more {
  margin-top: 0.4rem;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
