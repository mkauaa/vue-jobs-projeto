<script setup>
import Card from './Card.vue';
import { defineProps } from 'vue';


</script>

<template>
    <section class="py-4">
      <div class="container-xl lg:container m-auto">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 p-4 rounded-lg">
          <Card>
            <h2 class="text-2xl font-bold">Para desenvolvedores</h2>
            <p class="mt-2 mb-4">
              Navegue nossas vagas e inicie sua carreira hoje
            </p>
            <RouterLink
              to="/jobs"
              class="inline-block bg-black text-white rounded-lg px-4 py-2 hover:bg-gray-700"
            >
              Navegue vagas
            </RouterLink>
          </Card>
          <Card bg="bg-green-100">
            <h2 class="text-2xl font-bold">Para empregadores</h2>
            <p class="mt-2 mb-4">
              Anuncie sua vaga para encontrar o desenvolvedor perfeito
            </p>
            <RouterLink
              to="/jobs/add"
              class="inline-block bg-green-500 text-white rounded-lg px-4 py-2 hover:bg-green-600"
            >
              Adicionar Vaga
            </RouterLink>
          </Card>
        </div>
      </div>
    </section>
</template>