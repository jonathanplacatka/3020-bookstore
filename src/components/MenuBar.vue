<template>

  <!-- Menu Bar -->
  <v-app-bar color="primary" elevation="0">
    <a href="/" v-on:click="showHomepage.value = true" class="ms-5" style="align-items: center;">
      <img src="src\assets\Logo-text-white.png" style="height:50px">
    </a>
    <v-spacer></v-spacer>
    
    <h1 style="font-family: Caslon; margin-left: 10px; text-align: center; font-variant: small-caps;">Peaks Bookstore</h1>
    <v-spacer></v-spacer>

    <a href="/" v-on:click="showHomepage.value = true" style="align-items: center;">
    <v-btn color="white" icon>
      <v-icon icon="mdi-home" color="white" size="large"></v-icon>
    </v-btn></a>
      <v-btn color="white" icon> 
        <v-icon icon="mdi-account" color="white" size="large" id="menu-activator"></v-icon>
      </v-btn>


     <v-btn color="white" icon id="cart">
      <v-badge color="red" :content="totalItems" :model-value="totalItems > 0">
        <v-icon icon="mdi-cart" color="white" size="large" class=""></v-icon>
      </v-badge>


      <!-- Cart -->
      <v-menu v-model="isCartOpen" transition="slide-y-transition" activator="parent" :close-on-content-click="false">
        <v-card class="pa-2">
          <v-card-title class="text-center">
            Cart
            <v-btn icon="$close" variant="text" @click="isCartOpen = false" style="position: absolute; top: 0; right: 0;"></v-btn></v-card-title>
            <v-divider></v-divider>
          <v-row align="start" no-gutters>
            <v-list>

              <v-list-item v-if="totalItems <= 0">
                <v-list-item-title class="text-grey pa-1"><i>Your Cart is Empty</i></v-list-item-title>
              </v-list-item>

              <v-list-item v-for="(item, i) in items" :key="item.book.title" class="mb-2">
                <v-list-item-title class="text-left">{{ item.book.title }} <span v-if="!item.isPhysical">(Digital)</span> - <b>${{(item.selectedPrice * item.quantity).toFixed(2) }}</b> </v-list-item-title>

                <v-btn-group density="compact" divided variant="outlined" class="ml-6">
                  <v-btn :ripple="false" icon="mdi-minus" @click="decrement(i)"></v-btn>
                  <v-btn icon class="disable-events">{{ item.quantity }}</v-btn>
                  <v-btn :ripple="false" icon="mdi-plus" @click="increment(i)"></v-btn>
                </v-btn-group>

              </v-list-item>
              <v-list-item>
                <v-list-item-title class="text-left"> <b>Total: ${{ totalPrice }}</b></v-list-item-title>
              </v-list-item>
            </v-list>

          </v-row>

          <v-row no-gutters class="pb-4">
            <v-col align="center">
              <v-btn color="secondary" elevation="0" :disabled="totalItems <= 0">Checkout</v-btn>
            </v-col>
          </v-row>

        </v-card>
      </v-menu>

    </v-btn>

  </v-app-bar>
</template>

<script>
export default {
  data: () => ({
    items: [],
  isCartOpen: false,
  }),
  mounted() {
    this.emitter.on("add-to-cart", bookData => {
      this.addItem(bookData.book, bookData.isPhysical, bookData.selectedPrice)
    });
  },
  created() {
    if (localStorage.getItem('cartItems'))
      this.items = JSON.parse(localStorage.getItem('cartItems'));
  },
  watch: {
    items: {
      handler() {
        localStorage.setItem('cartItems', JSON.stringify(this.items))
      },
      deep: true,
    }
  },
  computed: {
    totalItems() {
      let sum = 0;
      this.items.forEach(item => { sum += item.quantity });
      return sum;
    },

    totalPrice() {
      let sum = 0;
      this.items.forEach(item => (sum += (item.selectedPrice * item.quantity)))
      return sum.toFixed(2);
    },

  },
  methods: {
    addItem(book, isPhysical, selectedPrice) {
      let result = this.items.find(item => (item.book.title === book.title && item.isPhysical == isPhysical))
      if (result) {
        result.quantity++
      } else {
        this.items.push({book: book, quantity: 1, isPhysical: isPhysical, selectedPrice: selectedPrice})
      }
    },

    increment(index) {
      this.items[index].quantity++;
    },

    decrement(index) {
      this.items[index].quantity--;
      if (this.items[index].quantity == 0) {
        this.items.splice(index, 1)
      }
    }
  }
}
</script>

<style scoped>
.disable-events {
  pointer-events: none;
}

</style>
