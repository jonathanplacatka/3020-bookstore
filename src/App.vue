<template>
  <v-app>
    <v-main>

      <MenuBar />

      <div class="search-box">

        <!-- does searching of the input when enter or search icon is pressed -->
        <input v-model="searchInput" @keydown.enter.prevent="doSearch" placeholder="Search" class="input-style" />


      </div>

      <v-sheet
        class="mx-10"
        elevation="0"
      >
        <div v-if="showHomepage">
          <BookSlideGroup title="Popular" tag="popular"/>
          <BookSlideGroup title="Recommended" tag="recommended"/>
          <BookSlideGroup title="First-Year" tag="firstyear"/>
          <BookSlideGroup title="Math" tag="math"/>
          <BookSlideGroup title="Arts" tag="arts"/>
          <BookSlideGroup title="Sciences" tag="science"/>
        </div>
        <div v-else>
          <h2> Search Results</h2>
          <div class="search-results">
            <BookCard v-for="(item, index) in searchResults" :key="index" :book="item" :title="props.title" />
          </div>
        </div>
      </v-sheet>

    </v-main>
  </v-app>
</template>


<style scoped>
.search-box {
  display: flex;
  justify-content: center;
  align-items: center;
}

.input-style {
  flex: 0.5;
  padding: 0.5rem;
  padding-left: 1rem;
  margin: 1.5rem;
  border: 2px solid rgb(102, 96, 96);
  border-radius: 2rem;
}

.search-results {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  padding: 1rem;
  margin: 1rem;
  justify-content: center;
  align-items: center;
}

h2 {
  margin-top: 0.5rem;
  margin-bottom: 1rem;
  margin-left: 3rem;
  padding-left: 3rem;
}
</style>


<script setup>
import BookSlideGroup from '@/components/BookSlideGroup.vue'
import MenuBar from '@/components/MenuBar.vue'
import BookCard from '@/components/BookCard.vue'
import books from '@/assets/books.json'

import { ref } from 'vue'
import { computed } from '@vue/reactivity'


const showHomepage = ref(true);
const searchInput = ref('');

//updates homepage depending on if there is no search input (show home page) or there is (show results)
const doSearch = () => {
  showHomepage.value = searchInput.value === '';
};

const props = defineProps(['title']);

// gets all the books that match the search input value
const searchResults = computed(() => {
  const searchInputLowerCase = searchInput.value.toLowerCase();

  return books.filter(book =>
    book.title.toLowerCase().includes(searchInputLowerCase) || book.author.toLowerCase().includes(searchInputLowerCase) ||
    book.isbn.toLowerCase().includes(searchInputLowerCase)
  );
});

</script>
