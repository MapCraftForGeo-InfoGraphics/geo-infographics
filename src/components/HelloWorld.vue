<template>
  <v-container style="width: 100%; height: 100%;">

    <v-navigation-drawer :width="400">
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
      <svg ref="svg" style="width: 100%; height: 100%;"></svg>
    </div>
  </v-container>
</template>

<script>
import * as d3 from 'd3';

export default {
  name: 'HelloWorld',

  data: () => ({
    mapData: {},
  }),

  mounted() {
    // 监听窗口大小变化
    window.addEventListener('resize', this.handleResize);

    // 初次渲染图表
    this.loadJson('countries.geojson').then(data => {
      this.mapData = data;

      this.loadJson('country-by-population.json').then(popuData => {
        this.mapData.features.forEach(feature => {
          var population = popuData.find(item => item.country === feature.properties.ADMIN);
          feature.properties.population = (population === undefined ? 0 : population.population);
        });

        console.log(this.mapData);
        this.handleResize(this.mapData);
      });
    });
  },

  beforeUnmount() {
    // 组件销毁时移除监听器
    window.removeEventListener('resize', this.handleResize);
  },

  methods: {
    handleResize() {
      this.drawChart(this.mapData);
    },

    drawChart(data) {
      const svg = d3.select(this.$refs.svg);

      // 移除现有的 SVG
      svg.selectAll('*').remove();

      const mapWidth = svg.node().getBoundingClientRect().width;
      const mapHeight = svg.node().getBoundingClientRect().height;

      const colorScale = d3.scaleSequential(d3.interpolateViridis)
          .domain([0, d3.max(data.features, d => d.properties.population)])
          .interpolator(d3.interpolateBlues);

      const projection = d3.geoMercator().fitSize([mapWidth, mapHeight], data);
      const path = d3.geoPath().projection(projection);

      svg.selectAll('path')
        .data(data.features)
        .enter()
        .append('path')
        .attr('d', path)
        .attr('fill', d => colorScale(d.properties.population))
        .attr('stroke', '#000000');
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
}

</script>
