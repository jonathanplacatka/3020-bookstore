<template>
  <v-card
    class="ma-4"
    width="140"
    height="200"
    elevation="0"
    :image="book.cover"
  >

  <v-dialog
        v-model="dialog"
        activator="parent"
        width="auto"
      >
        <v-card>
          <v-card-text>
            {{ book.title }}
          </v-card-text>
          <v-card-actions>
            <v-btn color="primary" block @click="dialog = false">Close Dialog</v-btn>
          </v-card-actions>
        </v-card>
    </v-dialog>

  </v-card>
</template>


<script>
  export default {
    props: ['book'],
    data: () => ({
      dialog: false,
    }),
  }
</script>