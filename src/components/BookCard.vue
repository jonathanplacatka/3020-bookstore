<template>
  <v-card
    class="ma-4"
    width="140"
    height="200"
    elevation="0"
    theme="dark"
    :image="cover"
  >

  </v-card>
</template>


<script>
  export default {
    props: ['cover'],
    data: () => ({
      model: null,
    }),
  }
</script>