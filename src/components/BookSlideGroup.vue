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
          :book="item"
        />
      </v-slide-group-item>
    </v-slide-group>
  </v-sheet>
</template>

<script>
  import BookCard from './BookCard.vue'
  import books from '../assets/books.json'
  export default {
    components: {
        BookCard
    },
    props: ['title'],
    data: () => ({
      model: null,
      booklist: books.slice().sort((a,b) => 0.5 - Math.random())
    }),
  }

  
</script>