<template>
  <v-app>
    <v-main>
      <MenuBar/>
      <SearchBar/>
      <BookSlideGroup title="Popular"/>
      <BookSlideGroup title="Recommended"/>
      <BookPopup></BookPopup>
    </v-main>
  </v-app>
</template>

<script setup>
  import BookSlideGroup from '@/components/BookSlideGroup.vue'
  import MenuBar from '@/components/MenuBar.vue'
  import SearchBar from '@/components/SearchBar.vue'
  import BookPopup from '@/components/BookPopup.vue'
</script>
