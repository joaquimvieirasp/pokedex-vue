<script setup>

// Importação dos elementos vue-router
import { RouterLink, RouterView } from 'vue-router'

// Importação do Bootstrap
import 'bootstrap/dist/css/bootstrap.min.css';

// Importar estilo CSS
import './complementos/estilos.css';

// Importar componente de navegação
import BarraNavegacao from './componentes/BarraNavegacao.vue';

</script>

<template>
  <!-- Barra de navegação -->
  <BarraNavegacao></BarraNavegacao>

  <!-- Visualizar conteúdo das páginas -->

  <RouterView />
</template>
