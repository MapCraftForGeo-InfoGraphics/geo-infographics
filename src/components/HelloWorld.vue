<template>
  
  <div style="display: flex; height: 100%; width: 100%;">
    <v-card elevation="6" height="100%" width="35%" ref="card">
      <v-container style="display: flex; overflow-y: auto;" id="seContainer">
        <VisualSelector></VisualSelector>
      </v-container>
    </v-card>

    <D3Panel ref="d3PanelInstance"></D3Panel>
  </div>

  <v-app-bar :elevation="2">
    <v-app-bar-title>Geo-Info Graphics WebUI</v-app-bar-title>
    <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
  </v-app-bar>

</template>

<script>
import { ref, provide } from 'vue';
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

      const seContainer = document.getElementById('seContainer');
      seContainer.style.maxHeight = (0.99 * height) + "px";
    });
  },

  // 将函数提供的方法（我也不懂）
  setup() {
    const projection = (type) => {
      console.log("change projection to type", type);
      // Call D3Panel's setProjection method
      d3PanelInstance.value.setProjection(type);
      d3PanelInstance.value.initMap();
    };

    // Provide setProjection function to child components
    provide('projection', projection);

    // Reference to D3Panel component instance
    const d3PanelInstance = ref(null);

    return {
      d3PanelInstance
    };
  }
}

</script>

<style></style>