<template>
  <!-- Menu Bar -->
  <v-app-bar color="primary" elevation="0">
    <v-app-bar-nav-icon color="white" />

    <v-spacer></v-spacer>
    <a href="/" v-on:click="showHomepage.value = true" style="align-items: center;">
      <img src="src\assets\Peaks_Logo_3-removebg-preview.png" style="height:100px">
    </a>
    <v-spacer></v-spacer>

    <v-btn color="white" icon>
      <v-icon icon="mdi-account" color="white" size="large" id="menu-activator"></v-icon>
    </v-btn>


    <v-btn color="white" icon>
      <v-badge color="red" :content="totalItems" :model-value="totalItems > 0">
        <v-icon icon="mdi-cart" color="white" size="large" id="menu-activator"></v-icon>
      </v-badge>


      <!-- Cart -->
      <v-menu transition="slide-y-transition" activator="parent" :close-on-content-click="false">
        <v-card class="pa-2">
          <v-row align="start" no-gutters>
            <v-list>

              <v-list-item v-if="totalItems <= 0">
                <v-list-item-title class="text-grey pa-1"><i>Your Cart is Empty</i></v-list-item-title>
              </v-list-item>

              <v-list-item v-for="(item, i) in items" :key="item.book.title" class="mb-2">
                <v-list-item-title class="text-left">{{ item.book.title }} - <b>${{
                  (item.book.price * item.quantity).toFixed(2) }}</b> </v-list-item-title>

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
    items: []
  }),
  mounted() {
    this.emitter.on("add-to-cart", book => {
      this.addItem(book)
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
      this.items.forEach(item => (sum += (item.book.price * item.quantity)))
      return sum.toFixed(2);
    },

  },
  methods: {
    addItem(book) {
      let result = this.items.find(item => item.book.title === book.title)
      if (result) {
        result.quantity++
      } else {
        this.items.push({ book: book, quantity: 1 })
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
