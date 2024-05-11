<script>
import AppCard from './AppCard.vue'; 
import { store } from '../store';
export default {
    components: { AppCard },
    data () {
        return {
            store,
        }
    }
}
</script>
<template>
    
        <div class="container py-5" v-if="store.arrayFilm.length > 0">
            <h1 class="py-5">FILM</h1>
            <div class="row row-cols-1 row-cols-md-2 row-cols-lg-4">
                <!-- in v-show dico di mostrare l elemento corrennte quando ha la chiave poster_path -->
                <div class="col py-3" v-for="curFilm in store.arrayFilm" v-show="curFilm.poster_path" >
                       <AppCard :cardObj="curFilm" />    
                </div>
            </div>
        </div>
   

    
        <div class="container py-5" v-if="store.arraySerie.length > 0">
            <h1>SERIE TV</h1>
            <div class="row row-cols-1 row-cols-md-2 row-cols-lg-4">
                 <!-- in v-show dico di mostrare l elemento corrennte quando ha la chiave poster_path -->
                <div class="col py-3" v-for="curSerie in store.arraySerie" v-show="curSerie.poster_path">                   
                        <AppCard :cardObj="curSerie" />       
                </div>
            </div>
        </div>

   
    
    
</template>

<style>
</style>