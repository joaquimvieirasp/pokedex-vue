<!-- HTML -->

<!-- SCRIPT -->

<script setup>

// Importações
import { onMounted, ref } from "vue";

// Variavel para exibir o carregamento
let pokeball = ref(true);

// Vetor contendo os Pokemons
const vetor = ref([]);

// Variável para aramzenar o termo da filtragem
let termoFiltragem = ref('');

onMounted(async () => {

    //Opção 1 

    try {
        for (let indice = 152; indice <= 251; indice++) {
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

// Função para filtrar os Pokémons
function filtrar() {
    return vetor.value.filter(obj => obj.name.includes(termoFiltragem.value));
}

</script>

<!-- HTML -->
<template>

    <div class="pokeball" v-if="pokeball">
        <img src="../complementos/pokeball.gif" alt="">
    </div>

    <!-- <ul>
        <li v-for="pokemon in vetor" :key="pokemon.id">
            {{ pokemon.name }}
        </li>
    </ul>    -->


    <main class="container" v-if="!pokeball">


        {{ termoFiltragem }}
        <!-- Filtragem -->

        <div class="row">
            <div class="col-12">
                <input type="text" v-model="termoFiltragem" placeholder="Qual Pokémon você está procurando?"
                    class="form-control pesquisa">

                <p v-if="filtrar().length == 0">Não foi encontrado nenhum Pokémon</p>
                <p v-else-if="filtrar().length == 1">Foi encontrado apenas um Pokémon</p>
                <p v-else>Foram encontrados {{ filtrar().length }} Pokémons</p>
            </div>
        </div>

        <!-- Listagem -->

        <div class="row">

            <div class="col-12 col-sm-6 col-md-4 col-lg-3" v-for="v in filtrar()" :key="v.id">

                <div class="card" :class="v.types[0].type.name">
                    <img :src="v.sprites.other.home.front_default">
                    <p>{{ v.name }}</p>
                    <p>{{ v.types[0].type.name }}</p>
                </div>

            </div>

        </div>

    </main>

</template>
