<template>
  <div class="clearfix">
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
                <div>

                  <input type="radio" id="physical" value="physical" name="type-of-book"/>
                  <label for="physical">Physical:&emsp;${{ book.price }}</label><br>

                  <input type="radio" id="digital" value="digital"  name="type-of-book"/>
                  <label for="digital">Digital:&emsp;${{(book.price *0.66).toFixed(2)}}</label><br>

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
      this.emitter.emit('add-to-cart', this.book);
      this.dialog = false;
      
      document.getElementById('cart').animate(
        [{ transform: "scale(1)"}, {transform: "scale(1.25)"},  {transform: "scale(1)"}], 
        {delay: 200, duration: 600, iterations:1}
      );

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