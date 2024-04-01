<template>
    <h1>¿Quien es este Pókemon?</h1>
    <PokemonPicture />
    <PokemonOptions />
</template>

<script>
import PokemonPicture from '@/components/PokemonPicture.vue'
import PokemonOptions from '@/components/PokemonOptions.vue'
export default {
    components:{
        PokemonPicture,
        PokemonOptions
    },
}
</script>

