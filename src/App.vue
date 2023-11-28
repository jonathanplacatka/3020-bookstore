<template>
  <v-app>
    <v-main>
      <MenuBar />
      <!-- <SearchBar /> -->

      <div class="search-box">

        <!-- does searching of the input when enter or search icon is pressed -->
        <input v-model="searchInput" @input="onSearchInput" @keydown.enter.prevent="doSearch" placeholder="Search"
          class="input-style" />


      </div>

      <div v-if="showHomepage">
        <BookSlideGroup title="Popular" />
        <BookSlideGroup title="Recommended" />
      </div>

      <div v-else>
        <h2> Search Results</h2>

        <div class="search-results">
          <BookCard v-for="(item, index) in searchResults" :key="index" :book="item" :title="props.title" />
        </div>
      </div>

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
}
</style>


<script setup>
import BookSlideGroup from '@/components/BookSlideGroup.vue'
import MenuBar from '@/components/MenuBar.vue'
import BookCard from '@/components/BookCard.vue'
import books from '@/assets/books.json'

import SearchBar from '@/components/SearchBar.vue'
import { ref } from 'vue'
import { computed } from '@vue/reactivity'


const showHomepage = ref(true);
const searchInput = ref('');

//updates homepage depending on if there is no search input (show home page) or there is (show results)
const doSearch = () => {
  showHomepage.value = searchInput.value === '';
};

const props = defineProps(['title']);


const searchResults = computed(() => {
  const searchInputLowerCase = searchInput.value.toLowerCase();

  return books.filter(book =>
    book.title.toLowerCase().includes(searchInputLowerCase) || book.author.toLowerCase().includes(searchInputLowerCase) ||
    book.isbn.toLowerCase().includes(searchInputLowerCase)
  );
});

</script>
