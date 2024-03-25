<template>
  <div style="display: flex; height: 100%; width: 100%;">
    <v-card elevation="6" height="100%" width="40%" ref="card">
      <v-container style="display: flex; overflow-y: auto;" id="seContainer">
        <VisualSelector></VisualSelector>
      </v-container>
    </v-card>

    <D3Panel></D3Panel>
  </div>

  <v-app-bar :elevation="2">
    <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
    <v-app-bar-title>Geo-Info Graphics WebUI</v-app-bar-title>
  </v-app-bar>


  <!-- 
  <v-container fluid ma-0 pa-0 fill-height style="width: 100%; height: 100%; margin-left: 0; margin-right: 0">
    <D3Panel />
    
    <v-navigation-drawer :width="400" v-model="drawer" app>
      <VisualSelector />
      <v-divider></v-divider>
    </v-navigation-drawer>

    <v-app-bar :elevation="2">
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-app-bar-title>Geo-Info Graphics WebUI</v-app-bar-title>
    </v-app-bar>

  </v-container> -->

</template>

<script>
import D3Panel from './D3Panel.vue';
import VisualSelector from './Selector.vue'

export default {
  name: 'HelloWorld',

  components: {
    D3Panel,
    VisualSelector
  },

  data: () => ({
    drawer: true,
  }),

  mounted() {
    const cardEl = this.$refs.card.$el;
    this.$nextTick(() => {
      const height = cardEl.clientHeight;

      console.log(height);
      // const seContainer = this.$refs.seContainer;
      // seContainer.style.maxHeight = height + "px";

      const seContainer = document.getElementById('seContainer');
      seContainer.style.maxHeight = (0.99 * height) + "px";
    });
  },

  methods: {

  },
}

</script>

<style></style>