<template>
<div class="clearfix">
  <v-card
    class="ma-4"
    hover
    width="140"
    height="200"
    elevation="0"
    :image="book.cover"
    link
  >

  <v-dialog
        v-model="dialog"
        activator="parent"
        width=60%
      >
        <v-card>
          <v-card-title> {{ book.title }} </v-card-title>
          <v-card-text>
        
          <div style="display: flex; font-size:12px; width: 100%;">
            <div style="flex: 40%; padding-right: 16px;"> 
                <img :src=book.cover class="custom-image">
                <strong>{{ book.rating }}&nbsp</strong> 
                <v-rating
                half-increments
                hover
                readonly
                :length="5"
                :size="13"
                :model-value=book.rating
                active-color="warning"
                />
            </div>

            <div style="flex: 60%; font-size: 14px;">
              <br>
                <strong>Author:</strong> {{ book.author }}
              <br>
                <strong>ISBN:</strong> {{ book.isbn }}
              <br>
                <strong>Edition:</strong> {{ book.edition }}
              <br>
                <strong>Year:</strong> {{ book.year }}
              <br>
                <strong>Price:</strong> {{ book.price }}
              <br>
                <strong>Units available:</strong> {{ book.available }}
            </div>
            </div>
            <v-btn @click="addToCart()">
              Add to Cart
            </v-btn>
          </v-card-text>
          <v-card-actions>
            <v-btn color="primary" block @click="dialog = false">Close Dialog</v-btn>
          </v-card-actions>
        </v-card>
    </v-dialog>

  </v-card>
  </div>
</template>


<script>
  export default {
    props: ['book'],
    data: () => ({
      dialog: false,
    }),
    methods: {
      addToCart() {
        this.emitter.emit('add-to-cart', this.book);
      }
    }
  }
</script>

<style scoped>
.column {
  
  margin: 1%; 
  float: left;
}
.clearfix::after {
  content: "";
  clear: both;
  display: table;
}
.custom-image {
  width: 100%; 
  height: 200px;
  object-fit: contain;
  object-position: left;
}
</style>