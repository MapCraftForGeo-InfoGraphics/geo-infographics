<template>

  <v-app-bar :elevation="2">
    <v-app-bar-title>Geo-Info Graphics WebUI</v-app-bar-title>
    <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

    <template v-slot:extension>
      <v-tabs v-model="currentItem" fixed-tabs>
        <v-tab :value="'home'">
          <v-icon>mdi-home</v-icon>
        </v-tab>

        <v-tab v-for="item in items" :key="item" :value="'tab-' + item">
          {{ item }}
        </v-tab>

        <v-menu v-if="more.length">
          <template v-slot:activator="{ props }">
            <v-btn class="align-self-center me-4" height="100%" rounded="0" variant="plain" v-bind="props">
              more
              <v-icon end>
                mdi-menu-down
              </v-icon>
            </v-btn>
          </template>

          <v-list class="bg-grey-lighten-3">
            <v-list-item v-for="item in more" :key="item" @click="addItem(item)">
              {{ item }}
            </v-list-item>
          </v-list>
        </v-menu>
      </v-tabs>
    </template>
  </v-app-bar>

  <v-window v-model="currentItem" style="height: 100%; width: 100%;">
    <v-window-item :value="'home'" style="display: flex; height: 100%; width: 100%;">
      <homeTab></homeTab>
    </v-window-item>

    <v-window-item :value="'tab-country-by-population'" style="display: flex; height: 100%; width: 100%;">
      <instanceTab></instanceTab>
    </v-window-item>
  </v-window>

  <!-- <instanceTab></instanceTab> -->

</template>

<script>
// import { ref, provide } from 'vue';
// import D3Panel from './D3Panel.vue';
// import VisualSelector from './Selector.vue'
import homeTab from './home.vue'
import instanceTab from './instance.vue'

export default {
  name: 'HelloWorld',

  components: {
    // D3Panel,
    // VisualSelector,
    homeTab,
    instanceTab
  },

  data: () => ({
    drawer: true,

    currentItem: 'home',
    items: [
      'country-by-population',
    ],
    more: [],
  }),

  methods: {
    addItem(item) {
      const removed = this.items.splice(-1, 1)
      this.items.unshift(
        ...this.more.splice(this.more.indexOf(item), 1),
      )
      this.more.unshift(...removed)
      this.$nextTick(() => { this.currentItem = 'tab-' + item })
    },
  },

  mounted() {
  },
}

</script>

<style></style>