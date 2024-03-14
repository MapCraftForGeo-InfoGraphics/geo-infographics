<template>
  <v-container style="width: 100%; height: 100%;">

    <v-navigation-drawer :width="400">
      <v-list-item title="Geo-Info Graphics" ></v-list-item>
      <v-divider></v-divider>

      <v-expansion-panels>
        <v-expansion-panel>
          <v-expansion-panel-title>
            item 1
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
            item 2
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
            item 3
          </v-expansion-panel-title>

          <v-expansion-panel-text>
            Some content 3
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

      this.loadJson('country-by-population.json').then(scale => {
        console.log(scale);
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

      const projection = d3.geoMercator().fitSize([mapWidth, mapHeight], data);
      const path = d3.geoPath().projection(projection);

      svg.selectAll('path')
        .data(data.features)
        .enter()
        .append('path')
        .attr('d', path)
        .attr('fill', 'lightgray')
        .attr('stroke', 'white');
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
