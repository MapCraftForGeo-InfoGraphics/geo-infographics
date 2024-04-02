<template>
  <v-app>
    <v-main>
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
                <v-btn class="align-self-center me-4" height="100%" width="fit-content" rounded="0" variant="plain"
                  v-bind="props">
                  <v-icon>mdi-menu-down</v-icon>
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

        <v-window-item v-for="item in items.concat(more)" :key="item" :value="'tab-' + item"
          style="display: flex; height: 100%; width: 100%;">
          <instanceTab :value="item" :geoData="geoData" :infoData="infoData"></instanceTab>
        </v-window-item>
      </v-window>

    </v-main>
  </v-app>
</template>

<script>
import * as d3 from 'd3';

import homeTab from './components/home.vue'
import instanceTab from './components/instance.vue'

export default {
  name: 'App',

  components: {
    homeTab,
    instanceTab
  },

  data: () => ({
    drawer: true,

    currentItem: 'home',
    items: [
      'country-by-population', 'abcde',
    ],
    more: ['hijkl'],

    geoData: {},
    infoData: {},
    userData: {},
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

    loadJson(na) {
      return new Promise((resolve, reject) => {
        d3.json(na).then(data => {
          resolve(data);
        }).catch(error => {
          console.error('Error loading GeoJSON data:', error);
          reject(error);
        });
      });
    },
  },

  mounted() {
    Promise.all([
      this.loadJson('countries.geojson'),
      this.loadJson('country-by-population.json')
    ])

      .then(([geoData, infoData]) => {
        this.geoData = geoData;
        this.infoData = infoData;
        console.log("geo-data loaded!")
      })
  },
}
</script>
