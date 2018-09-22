<template>
  <div id="app">
      
      <div class="header container">
        <div class="row">
          <div class="col-md-12">
            <!-- llama al componenete de la barra de nevegación -->
            <navbar @inicio="inicio" @recomendados="recomendados" @estrenos="estrenos" @populares="populares"> </navbar>
          </div>
        </div>

        <div class="container">
          <div class="row">
            <div class="col-md-12">
               <!-- llama al componenete de busqueda -->
              <search @busqueda="buscar"></search>
            </div>
          </div>
        </div>
      </div>

      <div class="container">
        <!-- mientras busca pone un spinner -->
        <spinner v-if="isLoading"></spinner>

        <!-- si el array de peliculas esta vacío pone un cartel para volver al inicio -->
        <div v-else-if="!movies">
          <p  style="padding:50px; background-color: #01d277; color: #FFF;">
          <i class="fas fa-exclamation-circle"></i> 
          No se encontraron peliculas. <a @click="inicio()">Volver al <b>inicio</b>.</a></p>
        </div>

        <!-- si el array de peliculas no esta vacío llama al componente preview que muestra las pelis en una card -->
        <div v-else class="container" style="padding-top:45px; padding-bottom:30px;">   
          <preview :movies="movies"></preview>
        </div>
      </div>
    
    <div>
      <!-- Footer -->
      <footer class="page-footer font-small black">

      <!-- autora -->
      <div class="footer-copyright text-center py-3">Gisela Gimenez
        <a href="https://github.com/GiselaGimenez/theMovieDB-finalProgAvanzada.git"> Proyecto en github</a>
      </div>

      </footer>
    <!-- Footer -->
    </div>

  </div>
</template>


<script>
import Spinner from './components/Spinner.vue';
import Search from './components/Search.vue';
import Preview from './components/Preview.vue';
import Navbar from './components/Navbar.vue';
const apiBaseUrl = 'https:\\api.themoviedb.org/3';
const apiKey = '50b6b4b3de11d4238953526155bf1747';

export default {
    name: 'app',
    components: { Search , Preview , Spinner, Navbar},
    
    data() {
      return{
        spinner: {size:50, status: true },
        isLoading: true,
        movies: []
      }
    },

    created() {
      this.sendQuery("/movie/now_playing?");
    },

    methods:{
      sendQuery(queryUrl) { // método principal que carga el array movies según la consulta que se hace
        this.isLoading = true;
        fetch(`${apiBaseUrl}${queryUrl}api_key=${apiKey}&language=es-ES`)
          .then((res) => {
            return res.json();
          })
          .then((res) => {
            this.isLoading = false;
            this.movies = res.results;
          })
        },
        
        buscar(query){// busca peliculas según la query
          this.sendQuery(`/search/movie?query=${query}&`)
        },

        inicio (){//muetra las peliculas en cartelera
          this.sendQuery(`/movie/now_playing?`);
        },

        recomendados (){//muestra las peliculas mejor valoradas
          this.sendQuery(`/movie/top_rated?`)
        },
      
        estrenos (){//muestra los próximos estrenos
          this.sendQuery(`/trending/movie/day?`)
        },

        populares (){//muestra las peliculas mas populares
          this.sendQuery(`/movie/popular?`)
        }
      },
}
</script>


<style lang="scss">
  @import '~bootstrap/dist/css/bootstrap.css';
  @import '~bootstrap-vue/dist/bootstrap-vue.css';

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  .header{
    background:#191919;
    padding-bottom: 25px;
  }
  body{
    width: 100%;
    border: 0;
  }
</style>
