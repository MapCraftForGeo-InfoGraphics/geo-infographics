<template>
  <v-container style="width: 100%; height: 100%;">

    <v-navigation-drawer 
      :width="320">
      <v-list-item title="Geo-Info Graphics WebUI" ></v-list-item>
      <v-divider></v-divider>

      <v-expansion-panels>
        <v-expansion-panel>

          <v-expansion-panel-title>
            Basci Map Representations
          </v-expansion-panel-title>
          <v-expansion-panel-text>
            Some content 1
            <v-img
              :src="require('../assets/logo.svg')"
              class="my-3"
              contain
              height="200"
            />
          </v-expansion-panel-text>
        </v-expansion-panel>


        <v-expansion-panel>
          <v-expansion-panel-title>
            Map Projections
          </v-expansion-panel-title>
          <v-expansion-panel-text>
            Some content 2
            <v-img
              :src="require('../assets/logo.svg')"
              class="my-3"
              contain
              height="200"
            />
          </v-expansion-panel-text>
        </v-expansion-panel>


        <v-expansion-panel>
          <v-expansion-panel-title>
            Hightlight Techniques
          </v-expansion-panel-title>
          <v-expansion-panel-text>
            Some content 3
          </v-expansion-panel-text>
        </v-expansion-panel>



        <v-expansion-panel>
          <v-expansion-panel-title>
            Label Positions
          </v-expansion-panel-title>
          <v-expansion-panel-text>
            Some content 4
          </v-expansion-panel-text>
        </v-expansion-panel>


        <v-expansion-panel>
          <v-expansion-panel-title>
            Encoding Channels
          </v-expansion-panel-title>
          <v-expansion-panel-text>
            Some content 5
          </v-expansion-panel-text>
        </v-expansion-panel>

      </v-expansion-panels>
    </v-navigation-drawer>
    


    <div ref="mapContainer" class="map-container" style="width: 100%; height: 100%;">
      <D3Panel></D3Panel>
    </div>
  </v-container>
</template>

<script>
import D3Panel from './D3Panel.vue';

export default {
  name: 'HelloWorld',
  
  components: {
    D3Panel
  },

  data: () => ({
    
  }),

  mounted() {

  },

  methods: {

  },
}

</script>
