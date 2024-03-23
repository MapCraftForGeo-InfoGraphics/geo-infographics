<template>

  <v-container fluid ma-0 pa-0 fill-height style="width: 100%; height: 100%; margin-left: 0; margin-right: 0">
    <D3Panel />

    <v-navigation-drawer :width="400" v-model="drawer" app>
      <ChannelSelector />
      <v-divider></v-divider>
    </v-navigation-drawer>

    <v-app-bar :elevation="2">
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-app-bar-title>Geo-Info Graphics WebUI</v-app-bar-title>
    </v-app-bar>

  </v-container>
</template>

<script>
import D3Panel from './D3Panel.vue';
import ChannelSelector from './Selector.vue'

export default {
  name: 'HelloWorld',

  components: {
    D3Panel,
    ChannelSelector
  },

  data: () => ({
    drawer: true,
  }),

  mounted() {

  },

  methods: {

  },
}

</script>
