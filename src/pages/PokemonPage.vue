<template>
    <h1 v-if="!pokemon">Cargando...</h1>
    <div v-else>
        <h1>¿Quién es este Pókemon?</h1>
        <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
        <PokemonOptions :pokemons="pokemonArr" @selection="checkAnswer" />

        <template v-if="showAnswer">
            <h2 class="fade-in">{{ message }}</h2>
            <button @click="newGame">
                Nuevo Juego
            </button>
        </template>
    </div>
</template>

<script>
import PokemonPicture from '@/components/PokemonPicture.vue'
import PokemonOptions from '@/components/PokemonOptions.vue'
import getPokemonOptions from '@/helpers/getPokemonOptions.js'


export default {
    components:{ PokemonPicture, PokemonOptions },
    data(){
        return {
            pokemonArr: [],
            pokemon:null,
            showPokemon: false,
            showAnswer: false,
            message: ''
        }
    },
    methods:{
        async mixPokemonArray(){
            this.pokemonArr = await getPokemonOptions()
            const rndInt = Math.floor(Math.random() * 4)
            this.pokemon = this.pokemonArr[ rndInt ]
        },
        checkAnswer( PokemonId ){
            this.showPokemon = true
            this.showAnswer = true
            if( this.pokemon.id === PokemonId ){
                this.message = 'Correcto!'
            }else {
                this.message = 'Oops, era ' + this.pokemon.name
            };
        },
        newGame(){
            this.showPokemon = false
            this.showAnswer = false
            this.pokemonArr = []
            this.pokemon = null
            this.message = ''
            this.mixPokemonArray()
        },
    },
    mounted(){
        this.mixPokemonArray()

    },
}
</script>

