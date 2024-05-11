<script>
export default {
    data() {
        return {
            flag: ["en", "es", "fr", "it", "question"],
            iconStar: []
        }
    },
    props: {
        cardObj: Object // in questo caso specifico è l'oggetto iesimo della lista di di fil/serie ritornate dall api
    },
    methods: {
        imagePoster() {
            // Funzione che mi permette di stampare dinamicamente la locandina del film e della serie corrente
            // Con il template literals
            // aggiungo nel return 
            return `https://image.tmdb.org/t/p/w342${this.cardObj.poster_path}`
        },
        getImgFlag(imgNameFlag) {
            return new URL(`${imgNameFlag}`, import.meta.url).href;
        },
        flagImage(imgFlag) {
            switch (imgFlag) {
                case "en": this.flag = '../assets/img/en.png'
                    return this.getImgFlag(this.flag);

                case "es": this.flag = '../assets/img/es.png'
                    return this.getImgFlag(this.flag);

                case "fr": this.flag = '../assets/img/fr.png'
                    return this.getImgFlag(this.flag);

                case "it": this.flag = '../assets/img/it.png'
                    return this.getImgFlag(this.flag);

                default: this.flag = '../assets/img/int.png'
                    return this.getImgFlag(this.flag);
            }
        },
        titleCard() {
            // operatore ternario visto che vado a creare una sola card sia per i film che per le serie tv
            // che hanno rispettivamente la chiave titolo diversa.
            // Dunque per le carte film stampa original title nemtre per le serie stampa name
            return this.cardObj.original_title ? this.cardObj.original_title : this.cardObj.name;
        },
    },
    computed: {
        valutation () {
            let star;
            return star = Math.round(this.cardObj.vote_average / 2);
            
        }
    }
}
</script>

<template>
    <div class="card w-100 h-100 border border-0 rounded bg-dark">
        <div class="ms_card-front position-relative w-100 h-100 rounded">
            <!-- Nell card front della mia immagine richiamo la funzione imagePoster che verrà stampata dinamicamente -->
            <img class="w-100 h-100 rounded" :src="`${imagePoster()}`" alt="">
        </div>

        <div class="ms_card-back position-absolute top-0 star-0 bg-dark w-100 h-100 text-light rounded">
            <h5  class="py-2 px-2  ">{{ titleCard() }}</h5>
            <h6  class="px-2  ">{{ cardObj.title }}</h6>
            <img class="py-2 px-2  "  :src="flagImage(cardObj.original_language)" alt="">
            <h5  class="py-1 px-2  d-flex flex-row">
                <div  v-for="i in valutation">
                    <span><i class="fa-solid fa-star "></i></span>
                </div>
                <div v-for="i in 5 - valutation ">
                    <span><i class="fa-regular fa-star"></i></span>
                </div>
            </h5>
            <p class="py-2 px-2 overflow-y-auto h-50">{{ cardObj.overview }}</p>
        </div>
    </div>
</template>

<style scoped lang="scss">
.ms_card-front,
.ms_card-back {
    transition: transform 0.8s;
    transform-style: preserve-3d;
}
.ms_card-back {
    opacity: 0;
    transform: rotateY(180deg);
    img {
        width: 20%;
    }
}
.card:hover .ms_card-front {
    transform: rotateY(180deg);
    z-index: -1;
}

.card:hover .ms_card-back {
    transform: rotateY(360deg);
    z-index: 1;
    opacity: 100%;
}
</style>