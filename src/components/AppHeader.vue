<script>
import { store } from "../store";
export default {
    data() {
        return {
            store
        }
    }
}
</script>

<template>

    <nav class="navbar bg-dark position-fixed top-0 star-0 w-100 z-2">
        <div class="container">
            <a class="navbar-brand text-danger fw-bold fs-3">BOOTFLIX</a>
            <div class="d-flex" role="search">
                <input class="form-control me-2" type="text" v-model="store.querySearch" aria-label="search"
                    placeholder="cerca...">
                <button class="btn btn-outline-danger" @click="$emit('search')">Cerca</button>    
            </div>
        </div>
    </nav>

  
</template>

<style></style>