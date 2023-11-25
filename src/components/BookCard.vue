<template>
  <v-card
    class="ma-4"
    width="140"
    height="200"
    elevation="0"
    theme="dark"
    :image="book.cover"
  >
  </v-card>
</template>


<script>
  export default {
    props: ['book'],
    data: () => ({
      model: null,
    }),
  }
</script>