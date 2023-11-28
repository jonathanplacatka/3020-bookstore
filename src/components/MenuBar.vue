<template>
      <v-app-bar style="background-color: MediumSeaGreen" elevation="0" class="px-auto">
          <v-app-bar-nav-icon color="white"/>
          <v-badge 
            color="red"
            :content="items.length"
            :model-value="items.length > 0"
          >
            <v-icon icon="mdi-cart" color="white" size="large" id="menu-activator"></v-icon>
          </v-badge>

          <a href="/" v-on:click="showHomepage = true" style="align-items: center; position: absolute; left:50%">
            <img src="src\assets\logo.svg" style=" width:40px;">
          </a>

      </v-app-bar>


      <v-menu
        transition="slide-y-transition"
        activator="#menu-activator"
      >
        <v-list>
          <v-list-item
            v-for="(item, i) in items"
            :key="i"
          >
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>

</template>

<script>
  export default {
    data: () => ({
      items: [],
    }),
    mounted() { 
      this.emitter.on("add-to-cart", book => {
        this.items.push(book);
      });
    }
  }
</script>