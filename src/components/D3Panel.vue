<template>
    <svg ref="svg" style="width: 100%; height: 100%;"></svg>
</template>

<script>
import * as d3 from 'd3';

export default {
  name: 'D3Panel',

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