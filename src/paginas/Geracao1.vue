<!-- SCRIPT -->

<script setup>

// Importações
import { onMounted, ref } from "vue";

// Variavel para exibir o carregamento
let carregamento = ref(true);

// Vetor contendo os Pokemons
const vetor = ref([]);

onMounted(async () => {

    //Opção 1 

    try {
        for (let indice = 1; indice <= 151; indice++) {
            const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${indice}`);
            const data = await response.json();
            vetor.value.push(data);
        }
    } catch (error) {
        console.error("Erro ao buscar dados:", error);
    }

    

    // Opção 2 do professor

    // for(let indice =1; indice <= 151; indice++){
    //     let requisicao = await fetch('https://pokeapi.co/api/v2/pokemon/1'+indice)
    //     let pokemon = await requisicao.json();
    //     vetor.value.push(pokemon);
    // }

    pokeball.value = false;

});
</script>

<!-- HTML -->
<template>

    <h1>Primeira geração</h1>

    <!-- <ul>
        <li v-for="pokemon in vetor" :key="pokemon.id">
            {{ pokemon.name }}
        </li>
    </ul>    -->

    <div class="pokeball" v-if="pokeball">
        <img src="../complementos/pokeball.gif" alt="">
    </div>


    <main class="container" v-if="!pokeball">

        <div class="row">

            <div class="col-12 col-sm-6 col-md-4 col-lg-3" v-for="v in vetor">

                <div class="card" :class="v.types[0].type.name">
                    <img :src="v.sprites.other.home.front_default">
                    <p>{{ v.name }}</p>
                    <p>{{ v.types[0].type.name }}</p>
                </div>

            </div>

        </div>

    </main>

</template>
