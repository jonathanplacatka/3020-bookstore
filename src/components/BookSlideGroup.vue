<template>
  <v-sheet
    elevation="0"
  >
    <h2>{{ title }}</h2>

    <v-slide-group
      show-arrows="always"
    >
      <v-slide-group-item>
        <BookCard 
          v-for="(item, index) in filtered"
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
    props: ['title', 'tag'], 
    computed: {
      filtered() {
        return books.filter((book) => book.tags.includes(this.tag)).sort((a,b) => 0.5 - Math.random())
      }
    }
  }
</script>

<style>
  .v-slide-group__next, .v-slide-group__prev {
    height: 260px !important;   
  }
</style>