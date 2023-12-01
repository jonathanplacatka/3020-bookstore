<template>
  <div>
    <v-card elevation="0" width="140" height="270" class="mx-4 my-2">
      <v-card
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
            width=40%
        >
          <v-card class="content">
            <v-card-item>
              <v-btn icon="$close" variant="text" @click="dialog = false" style="position: absolute; top: 2px; right: 2px;"></v-btn>
            </v-card-item>
            
            <v-card-item>
              <h2> {{ book.title }}</h2>
            </v-card-item>

            <div>
            </div>
  
            
            <v-card-text class="book-details-container">
                
                <img :src=book.cover class="custom-image">

                <div class="book-details-text">
                  <br>
                    <strong>Author:</strong> {{ book.author }}
                  <br>
                    <strong>ISBN:</strong> {{ book.isbn }}
                  <br>
                    <strong>Year:</strong> {{ book.year }}
                  <br>
                  <strong>Rating: </strong>
                  <br>
                    <v-rating
                    half-increments
                    hover
                    readonly
                    :length="5"
                    :size="20"
                    :model-value=book.rating
                    active-color="warning"
                    />
                  <br>
                  
                 </div>
              </v-card-text>

              <v-divider class="mx-5 mt-4"></v-divider>

              <div class="bottom-container">

                <div class="price-selector">
                  <input type="radio" id="physical" value="physical" name="type-of-book" checked/>
                  <label for="physical"> Physical: ${{ book.price }}</label><br>

                  <input type="radio" id="digital" value="digital" name="type-of-book" />
                  <label for="digital"> Digital: ${{book.eprice}}</label>
                </div>


                  <v-spacer></v-spacer>
                  <v-btn class="cart-button" elevation="0" color="secondary" @click="addToCart()">Add to Cart</v-btn>
              
          
                  
              </div>
      

          </v-card>
      </v-dialog>
    </v-card>
    <div class="sub-text">
      <p class="book-title">{{ book.title }}</p>
      <p class="author"><i>{{ book.author }}</i></p> 
    </div>
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
      let isPhysical = document.querySelector('input[name=type-of-book]:checked').value == 'physical'
      let selectedPrice = isPhysical ? this.book.price : this.book.eprice
      this.emitter.emit('add-to-cart', {book: this.book, isPhysical: isPhysical, selectedPrice: selectedPrice});
      this.dialog = false;

      console.log(isPhysical) 
      
      document.getElementById('cart').animate(
        [{ transform: "scale(1)"}, {transform: "scale(1.25)"},  {transform: "scale(1)"}], 
        {delay: 200, duration: 600, iterations:1}
      );

    }
  }
}
</script>

<style scoped>


.content {
  display: flex;
  flex-direction: column;
  padding-left: 6px;
  padding-right: 6px;
}

.book-details-container {
  display: flex;
  flex-direction: row;
}

.book-details-text {
  font-size: 18px;
  margin-left: 35px;
}

.bottom-container {
  display: flex;
  flex-direction: row;
  align-content: center;
  margin: 20px
}

.price-selector {
  font-size: 18px;
}

.cart-button {
  margin-top: 9px;
}

.custom-image {
  width: 175px;
  height: 250px;
}

.sub-text {
  margin-top: 4px;
  text-align: center;
}

.book-title  {
  width: 140px;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  overflow: hidden;
  color: black;
}

.author {
  width: 140px;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 1;
  overflow: hidden;
  color: grey;
  font-size: 14px;
}
</style>