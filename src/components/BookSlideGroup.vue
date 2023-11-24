<template>
  <v-sheet
    class="mx-auto"
    elevation="0"
    max-width="1350"
  >
    <h2>{{ title }}</h2>

    <v-slide-group
      v-model="model"
      selected-class="bg-success"
      show-arrows
    >
      <v-slide-group-item>
        <BookCard 
          v-for="(item, index) in booklist"
          :key="index"
          :cover="item"
        />

      </v-slide-group-item>
    </v-slide-group>
  </v-sheet>
</template>

<script>
  import BookCard from './BookCard.vue'
  import { covers } from '../assets/booklist.js'
  export default {
    components: {
        BookCard
    },
    props: ['title'],
    data: () => ({
      model: null,
      booklist: covers.slice().sort((a,b) => 0.5 - Math.random())
    }),
  }

  
</script>