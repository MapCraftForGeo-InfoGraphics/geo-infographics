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
          <instanceTab :value="item" :geoData="geoData" :infoData="infoDatas[item]"></instanceTab>
        </v-window-item>
      </v-window>

    </v-main>
  </v-app>
</template>

<script>
import * as d3 from 'd3';
import { ref, provide } from 'vue';

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
    // items: [],
    more: [],

    geoData: {},
    userDatas: {},
  }),

  mounted() {
    this.loadJson('europe.geojson')
      .then((geoData) => {
        this.geoData = geoData;
        console.log("geo-data loaded!");
      })
  },

  setup() {
    const items = ref([]);
    const infoDatas = ref({});

    const uniqueName = (namesArray, name) => {
      let newName = name.replace(/\..+$/, '');
      let count = 1;

      // 检查数组中是否包含该名字，如果包含，则在名字后添加后缀
      while (namesArray.includes(newName)) {
        newName = `${name} (${count})`;
        count++;
      }

      return newName;
    }

    const loadInfoData = (file) => {
      const reader = new FileReader();
      reader.onload = function (e) {
        const fileContents = e.target.result; // 获取文件内容
        // 将文件内容传递给 d3.json() 函数
        d3.json(fileContents).then(data => {

          const infoData = data.reduce((acc, cur) => {
            acc[cur.country] = cur.annotation;
            return acc;
          }, {});

          const value = uniqueName(items.value, file.name)
          infoDatas.value[value] = infoData;
          items.value.unshift(value);

          // 处理加载的JSON数据
        }).catch(error => {
          // 处理加载数据时发生的错误
          console.error(error);
        });
      };

      reader.readAsDataURL(file);
    };

    provide('loadInfoData', loadInfoData);
    return {items, infoDatas};
  },

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

    uniqueName(namesArray, name) {
      let newName = name;
      let count = 1;

      // 检查数组中是否包含该名字，如果包含，则在名字后添加后缀
      while (namesArray.includes(newName)) {
        newName = `${name} (${count})`;
        count++;
      }

      return newName;
    }
  },
}
</script>
