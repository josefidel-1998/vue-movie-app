<template>
  <div class="home">
    <section class="seccion">
        <h2>Busca tus peliculas favoritas</h2>
    </section>
    <form @submit.prevent="searchMovies" class="search-box">
      <input type="text" placeholder="¿Que pelicula/serie estas buscando?" v-model="search" />
      <input type="submit" value="Search" />
    </form>
    <section class="movies">
      <article class="movie" v-for="movie in movies" :key="movie.imdbID">
          <router-link :to="'/movie/' + movie.imdbID" class="link">
              <figure class="product-image">
                <img :src="movie.Poster"  :alt="movie.Title" />
                  <figcaption class="type">
                      <h3>{{movie.Title}}</h3>
                      <h4>{{movie.year}}</h4>
                      <p>{{movie.Type}}</p>
                  </figcaption>
              </figure>
          </router-link>
      </article>
    </section>
  </div>
</template>

<script>

  import {ref} from 'vue';
  //mport env from '@/env.js';

export default {
  name: 'HomeView',
  setup(){
    const search = ref("");

    const movies = ref([]);

    const apikey = '604c3d58';

    const searchMovies = () =>{
      if(search.value != ""){
        fetch(`http://www.omdbapi.com/?i=tt3896198&apikey=${apikey}&s=${search.value}`)
        .then(response => response.json())
        .then(data => {

            movies.value = data.Search;
            console.log(data)
        })
        search.value = '';
      }
    }
    return {
      search,
      movies,
      searchMovies,
      apikey,
    }
  }
}
</script>
<style lang="scss" scoped>
  .home{
    .seccion h2{
        color: white;
        text-align:center;
        margin: 2rem 0;
    }
    .search-box{
      display:flex;
      flex-direction: column;
      justify-content: center;
      padding: 1rem;
      align-items: center;

      input {
        display: block;
        appearance: none;
        border: none;
        outline: none;
        background-color:none;

        &[type="text"] {
          width: 100%;
          color: white;
          background-color:#496583;
          font-size: 1.2rem;
          padding: 0.8rem 1rem;
          border-radius: 9px;
          margin-block: 1rem;
          transition: all 0.4s;
          
          &::placeholder {
            color: #f3f3f3;
          }
          &:focus {
            box-shadow: 0,3px,6px rgba(0,0,0,0.5);
          }
        }
        &[type="submit"] {
          width: 100%;
          max-width: 300px;
          background-color:#428883;
          padding: 1rem;
          border-radius: 8px;
          color: white;
          font-size: 1.2rem;
          text-transform: uppercase;
          transition: all 0.4s;
          cursor: pointer;

          &:active{
            background-color: #3b8070;
          }
          &:hover{
            background-color: #215a56ac;
          }
        }
      }
    }
    .movies{
      width: 100%;
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      margin: auto;
      place-items: center;
      

    .movie{
      max-width: 100%;
      flex: 1 1 100%;
      padding: 1rem 0.5rem;

        .link{
          display: flex;
          flex-direction: column;
          height: 100%;

          .product-image{
            position: relative;
            display: block;

              img{
                display: block;
                width: 100%;
                object-fit: cover;
              }
              .type{
                width: 100%;
                position: absolute;
                bottom: 0;
                left: 0;
                padding-block: 1rem;
                background-color: #415049a8;
                h3,h4,p{
                  color: white;
                  text-align: center;
                }
              }

          }
        }
    }
    }
    @media screen and (max-width:768px){
      .movies{
        grid-template-columns: 1fr 1fr;
      }
    }
    @media screen and (max-width:450px){
      .movies{
        grid-template-columns: 1fr;
      }
    }
  }
</style>
