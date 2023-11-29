<template>
      <v-app-bar style="background-color: MediumSeaGreen" elevation="0">
          <v-app-bar-nav-icon color="white"/>
          <v-spacer></v-spacer>
          <v-badge 
            color="red"
            :content="numItems()"
            :model-value="items.length > 0"
            class="pr-6"
          >
            <v-icon icon="mdi-cart" color="white" size="large" id="menu-activator"></v-icon>
          </v-badge>

      </v-app-bar>

      <v-menu
        transition="slide-y-transition"
        activator="#menu-activator"
      >
        <v-card>
          <v-col
              align="center"
          >
            <v-list>
              <v-list-item
                v-for="(item, i) in items"
                :key="i"
              >
                <v-list-item-title class="text-left">{{ item.book.title }} ({{ item.quantity }}) - <b>${{ item.book.price }}</b> </v-list-item-title>
              </v-list-item>
              <v-list-item>
                <v-list-item-title class="text-left"> <b>Total: {{ this.total() }}</b></v-list-item-title>
              </v-list-item>
            </v-list>

            <v-btn>Checkout</v-btn>

          </v-col>
        </v-card>
      </v-menu>
</template>

<script>
  export default {
    data: () => ({
      items: [],
    }),
    mounted() { 
      this.emitter.on("add-to-cart", book => {
        this.addItem(book)
      });
    },
    methods: {
      addItem(book) {
        let result = this.items.find(item => item.book === book) 
        if(result) {        
          result.quantity++
        } else {
          this.items.push({book: book, quantity: 1})
        }
      },
      numItems() {
        let sum = 0;
        this.items.forEach(item => {sum += item.quantity});
        return sum;
      },
      total() {
        let sum = 0;
        this.items.forEach(item => (sum += (item.book.price*item.quantity)))
        return sum;
      }
    }
  }
</script>

