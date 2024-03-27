<template>
  <v-container style="width: 100%; height: 100%; margin-left: 0; margin-right: 0">
    <svg ref="svg" style="width: 100%; height: 100%;"></svg>
  </v-container>

</template>

<script>
import * as d3 from 'd3';

export default {
  name: 'D3Panel',

  data: () => ({
    svg: null,

    mapHeight: 100,
    mapWidth: 100,

    geoData: {},
    geoProjection: null,
    geoPath: null,

    myType: {
      "Political Map": 0,
      "Shape-based Map": 1,
      "Grid Cartogram": 2,
      "Topographic Map": 3,
      "Street Map": 4,

      "Mollweide": 0,
      "Robinson": 1,

      "Light": 0,
      "Color": 1,
      "Map Pin": 2,
      "3D Transformation": 3,
      "Enlarged Positions": 4,

      "Label Situated": 0,
      "Label Text": 1,

    }
  }),

  mounted() {
    // 获得html中的地图（svg）标签
    this.svg = d3.select(this.$refs.svg);

    //根据窗口大小设置地图的大小
    this.mapWidth = this.svg.node().getBoundingClientRect().width;
    this.mapHeight = this.svg.node().getBoundingClientRect().height;

    // 读取geojson
    this.loadJson('countries.geojson').then(data => {
      this.geoData = data;

      // 读取人口信息
      this.loadJson('country-by-population.json').then(popuData => {
        this.geoData.features.forEach(feature => {
          var population = popuData.find(item => item.country === feature.properties.ADMIN);
          feature.properties.population = (population === undefined ? 0 : population.population);
        });

        //配置默认数据
        this.setProjection(0);

        //绘制地图
        this.initMap();
      });
    });
  },

  methods: {
    //重新加载数据并绘制svg
    initMap() {
      this.geoPath = d3.geoPath().projection(this.geoProjection);
      this.drawSvg()
    },

    //重新绘制svg
    drawSvg() {
      // 移除现有的 SVG
      this.svg.selectAll('*').remove();

      // 设置色彩的Encoding Channel
      const colorScale = d3.scaleSequential(d3.interpolateViridis)
        .domain([0, Math.log(d3.max(this.geoData.features, d => d.properties.population))])
        .interpolator(d3.interpolateBlues);

      // 绘制svg
      this.svg.selectAll('path')
        .data(this.geoData.features)
        .enter()
        .append('path')
        .attr('d', this.geoPath)
        .attr('fill', d => colorScale(Math.log(d.properties.population)))
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

    // 

    // 设置 Map Representation
    setRepresentation(type) {
      console.log("Representation:", type)
    },

    // 设置 Map Projection
    // 0: Mollweide
    // 1: Robinson
    setProjection(type) {
      console.log("Map Projection:", type);

      if (type === this.myType['Mollweide']) {
        this.geoProjection = d3.geoProjection(function (x, y) {
          var lambda = x / 180 * Math.PI;
          var phi = y / 180 * Math.PI;
          var theta = Math.asin((2 * phi) / Math.PI);
          var _x = (Math.sqrt(2) / Math.PI) * lambda * Math.cos(theta);
          var _y = Math.sqrt(2) / Math.PI * Math.sin(theta);
          return [_x, _y];
        }).fitSize([this.mapWidth, this.mapHeight], this.geoData);
      }

      else if (type === this.myType['Robinson']) {
        this.geoProjection = d3.geoProjection(function (x, y) {
          // 投影函数
          var lambda = x / 180 * Math.PI;
          var phi = y / 180 * Math.PI;
          var phi_1 = Math.asin(2 / Math.PI * Math.sin(phi));
          var theta = 0.8 * lambda * Math.cos(phi_1);
          var _x = 2 / Math.PI * theta;
          var _y = Math.sin(phi_1);
          return [_x, _y];
        }).fitSize([this.mapWidth, this.mapHeight], this.geoData);
      }
    },

    setHighlight(type) {
      console.log("Highlight Techniques:", type)
    },

    setLabelPosition(type) {
      console.log("Label Position:", type)
    },

    setEncodingChannel(type) {
      console.log("Encoding Channel:", type)
    },

  },
}
</script>