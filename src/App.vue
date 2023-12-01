<template>
  <v-app>
    <v-main>

      <MenuBar/>
      <!-- does searching of the input when enter or search icon is pressed -->
      <div class="search-box">      
        <v-text-field
        density="compact"
        variant="outlined"
        label="Search by Title, Author, or ISBN..."
        append-inner-icon="mdi-magnify"
        single-line
        hide-details
        outlined
        v-model="searchInput"
        @keydown.enter="search"
        @click:append-inner="search"
        class="input-style"
      ></v-text-field>
      </div>

      <v-sheet class="content" elevation="0">
        <div v-if="showHomepage" class="categories-container">
          <BookSlideGroup title="Popular" tag="popular" />
          <BookSlideGroup title="Recommended" tag="recommended" />
          <BookSlideGroup title="First-Year" tag="firstyear" />
          <BookSlideGroup title="Math" tag="math" />
          <BookSlideGroup title="Arts" tag="arts" />
          <BookSlideGroup title="Sciences" tag="science" />
        </div>
        <div v-else class="">
          <h2 class="search-header"> Search Results</h2>
          <div class="search-results">
            <BookCard v-for="(item, index) in searchResults" :key="index" :book="item" :title="props.title" />
          </div>
        </div>
      </v-sheet>
      <v-footer color="accent"><v-spacer></v-spacer>2023 - PEAKS LLC</v-footer>

    </v-main>
  </v-app>
</template>
<style scoped>

.content {
  padding-left: 40px;
  padding-right: 40px;
  min-height: 100vh
}

.search-results {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(156px, max-content));
  grid-gap: 0px;
  justify-content: begin;
  padding: initial;
}

.search-box {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}

.search-header {
  margin-left: 16px;
}

.categories-container {
  display:flex;
  flex-direction: column;
  row-gap: 30px;
}

.input-style {
  flex: 0.5;
  padding: 0.5rem;
  padding-left: 1rem;
  margin: 1.5rem;

}

.footer {
  position: fixed;
  bottom: 0;
  width: 100%;
}
</style>


<script setup>
  import BookSlideGroup from '@/components/BookSlideGroup.vue'
  import MenuBar from '@/components/MenuBar.vue'
  import BookCard from '@/components/BookCard.vue'
  import books from '@/assets/books.json'

  import { ref } from 'vue'
 
  const showHomepage = ref(true);
  const searchInput = ref('');
  const searchResults = ref([]);

  const props = defineProps(['title']);

  // gets all the books that match the search input value
  const search = () => {
    const searchInputLowerCase = searchInput.value.toLowerCase();
    searchResults.value = books.filter(book =>
      book.title.toLowerCase().includes(searchInputLowerCase) || book.author.toLowerCase().includes(searchInputLowerCase) ||
      book.isbn.toLowerCase().includes(searchInputLowerCase)
    );
    showHomepage.value =  searchInput.value === '';;
  };

</script>
