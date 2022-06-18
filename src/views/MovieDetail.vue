<template>
    <section class="movie-detail">
        <h2>Detalles de la pelicula</h2>
            <figure class="card">
                <img :src="movie.Poster"  :alt="movie.Title" />
                  <figcaption class="type"> 
                      <h3>{{movie.Title}}</h3>
                      <h4>{{movie.year}}</h4>
                      <h5>{{movie.Type}}</h5>
                      <p>{{movie.Plot}}</p>
                  </figcaption>
            </figure>
    </section>
</template>

<script>
    import {onBeforeMount, ref} from 'vue';
    import {useRoute} from 'vue-router';

export default {
    setup(){
        const movie = ref({});
        const route = useRoute(); // aqui uso la ruta, tipo la ruta $route.params.id del html
        const apikey = '604c3d58';

        onBeforeMount(() =>{
            fetch(`http://www.omdbapi.com/?apikey=${apikey}&i=${route.params.id}&plot=full`)
            .then(response => response.json())
            .then(data =>{
                movie.value = data;
                console.log(data)
            })
        });
        return{
            route,movie,apikey
        }
    }
}
</script>

<style>
    .movie-detail h2{
         color: white;
         text-align: center;
         margin-block: 2rem;
    }
    .card{
        display: flex;
        flex: 1 1 100%;
        flex-direction: row;
        column-gap: 3rem;
        align-items: center;
        background-color: #496583;
        margin: auto;
    }
    .type{
        color: white;
        display: flex;
        flex-direction: column;
        row-gap: 1rem;
        margin: auto;
        justify-content: center;
        text-align: center;
        margin-inline-end: 1.5rem;
    }
    @media screen and (max-width:768px) {
        .card{
            flex-direction:column ;
        }
        .type{
            margin-top: 1.5rem;
            margin-inline-end: 0;
        }
    }
</style>