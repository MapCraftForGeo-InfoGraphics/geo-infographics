<template>

  <v-app-bar :elevation="2">
    <!-- <template v-slot:prepend>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
    </template> -->

    <v-app-bar-title>Geo-Info Graphics WebUI</v-app-bar-title>
  </v-app-bar>

  <v-container fluid ma-0 pa-0 fill-height style="width: 100%; height: 100%; margin-left: 0; margin-right: 0">
    <v-row
        align="start"
        style="height: 100%; width: 100%; margin-left: 0; margin-right: 0;"
      >
      <v-col cols="2" style="height: 100%; min-width: 300px;">
        <v-expansion-panels>
          <v-expansion-panel>

            <v-expansion-panel-title>
              Basic Map Representations
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
      </v-col>

      <v-col ref="mapContainer" class="map-container" style="width: 100%; height: 100%;">
        <D3Panel></D3Panel>
      </v-col>
      
    </v-row>

    <!-- <v-navigation-drawer 
      :width="320">
      <v-list-item title="Geo-Info Graphics WebUI" ></v-list-item>
      <v-divider></v-divider>

      
    </v-navigation-drawer> -->
    


    
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
