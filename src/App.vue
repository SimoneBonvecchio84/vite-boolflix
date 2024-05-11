<script>
import { store } from "./store";
import axios from "axios";
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
export default {
    components: {
      AppHeader,
      AppMain
    },
    data() {
      return {
        isLoading: false,
        store,
      }
    },
    methods: {
      searchMovie() {
        this.isLoading =true;
        console.log("ciao")
        // creo oggetto nel quale ho due chiavi corrispondenti a api_key e query trovate nella documentazione del sito nella 
        // sezione api
        // in queste due chiavi salvo in api_key la chiave d'accesso che mi permettera di ricevere i dati dei film
        // e in query salvo il valore querySearch che associato al v-model del mio imput mi permetterà di cercare i film e le serie 
        const paramsObj = {
          api_key: this.store.apiKey,
          query: this.store.querySearch,
        };

        // Chiamata Axios.
        // Creo due variabili nelle quali salvo i rispettivi link dei film e delle serie tv
        
        const movieReq = axios.get("https://api.themoviedb.org/3/search/movie", {
          params: paramsObj // inserisco i parametri 
        });

        const tvReq = axios.get("https://api.themoviedb.org/3/search/tv", {
          params: paramsObj
        });

        //sintassi Axios 
        // con questa sintassi nell array axios.all andiamo a salvare le due variabili movieReq e tvReq e applichiamo then come
        // da procedura standard
        // Alle variabili in store arrayFilm e arraySerie salviamo gli oggetti provenienti dal server resp[0] e resp[1].
        // Rispettivamente la lista dei film e quella delle serie
        axios.all([movieReq, tvReq]).then((resp) => {
          this.store.arrayFilm  = resp[0].data.results;
          this.store.arraySerie = resp[1].data.results;
          console.log(this.store.arrayFilm, "lista films");
          console.log(this.store.arraySerie, "lista Serie"); 
          this.store.querySearch = ""; // svuotare campo input dopo ricerca
        })

      }
    }
}
</script>

<template>
  <AppHeader @search="searchMovie"/>
  <AppMain />
</template>

<style>
</style>