<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movies/tt6468322">
        <img src="https://m.media-amazon.com/images/M/MV5BZDcxOGI0MDYtNTc5NS00NDUzLWFkOTItNDIxZjI0OTllNTljXkEyXkFqcGdeQXVyMTMxODk2OTU@._V1_SX300.jpg" alt="Money Heist Poster" class="featured-img" />
        <div class="detail">
          <h3>Money Heist</h3>
          <p>
            An unusual group of robbers attempt to carry out the most perfect robbery in Spanish history - 
            stealing 2.4 billion euros from the Royal Mint of Spain.
          </p>
        </div>
      </router-link>
    </div>

    <form @submit.prevent="searchMovies" class="search-box">
      <input type="text" placeholder="what are you looking for?" v-model="search" />
      <button type="submit">Search</button>
    </form>

    <clip-loader :loading="loading" :color="color" :size="size"></clip-loader>
    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movies/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster" />
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import ClipLoader from 'vue-spinner/src/ClipLoader.vue'

export default {
  components: {
    ClipLoader
  },
  setup(){
    const search = ref("");
    const loading = ref(false);
    const color = ref("#E50914");
    const movies = ref([]);
    const size = ref("100px");
    const searchMovies = () => {
      if(search.value != ""){
        movies.value = [];
        loading.value = true;
        fetch(`${process.env.VUE_APP_API_URL}?apikey=${process.env.VUE_APP_KEY}&s=${search.value}`)
          .then(res => res.json())
          .then(data => {
            movies.value = data.Search;
            loading.value = false;
            search.value = '';
          });
      }
    }

    return {
      search,
      movies,
      searchMovies,
      loading,
      color,
      size
    }
  }
}
</script>
<style lang="scss" scoped>
.home{
  padding-top: 50px;
  width: 100%;
  .feature-card{
    position: relative;

    .featured-img{
      display: block;
      width: 100%;
      height: 400px;
      object-fit: cover;
      position: relative;
      z-index: 0;
      object-position: 50% bottom;
    }

    .detail{
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;

      h3{
        color: #fff;
        margin-bottom: 16px;
      }

      p{
        color: #FFFFFF;
      }
    }
  }

  .search-box{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;

    input{
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;
      width: 100%;
      color: #fff;
      background-color: #131313;
      font-size: 20px;
      padding: 10px 16px;
      border-radius: 8px;
      margin-bottom: 15px;
      transition: 0.4s;

      &::placeholder{
        color: #f3f3f3;
      }

      &:focus{
        box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
      }
    }

    button{
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;
      width: 100%;
      max-width: 300px;
      background-color: #E50914;
      padding: 16px;
      color: #fff;
      border-radius: 8px;
      font-size: 20px;
      text-transform: uppercase;
      transition: 0.7s;

      &:active{
        background-color: #131313;
      }

    }
  }
  .movies-list{
    display: flex;
    flex-wrap: wrap;
    margin: 0px 8px;

    .movie{
      max-width: 50%;
      flex: 1 1 50%;
      padding: 16px 8px;

      .movie-link{
        display: flex;
        flex-direction: column;
        height: 100%;

        .product-image{
          position: relative;
          display: block;

          img{
            display: block;
            width: 100%;
            height: 275px;
            object-fit: cover;
          }

          .type{
            position: absolute;
            padding: 8px 16px;
            background-color: #E50914;
            color: #fff;
            bottom: 16px;
            left: 0px;
            text-transform: capitalize;
          }
        }

        .detail{
          background-color: #111111;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0px 0px 8px 8px;

          .year{
            color: #aaaaaa;
            font-size: 14px;
          }

          h3{
            color: #fff;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
  }
}
</style>

