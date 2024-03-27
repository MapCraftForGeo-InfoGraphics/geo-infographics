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

    fillColorFunction: () => '#808080', // 默认为单一灰色

    myType: {
      "Political Map": 0,
      "Topographic Map": 1,
      "Shape-based Map": 2,
      "Street Map": 3,
      "Grid Cartogram": 4,


      "Mollweide": 0,
      "Robinson": 1,

      "Light": 0,
      "Color": 1,
      "Map Pin": 2,
      "3D Transformation": 3,
      "Enlarged Positions": 4,

      "Label Situated": 0,
      "Label Text": 1,
      "Label Icon": 2,
      "Label Color": 3,
      "Label Convenient": 4,
      "Label Aligned": 5,
      "Label Ordered": 6,

      "Color (Luminance)": 0,
      "Color (Hue)": 1,
      "3D Length": 2,
      "Glyph": 3,
      "Link (Line)": 4,
      "Link (Arrow)": 5,
      "Size": 6,
      "Quantity": 7,



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

      // // 设置色彩的Encoding Channel
      // const colorScale = d3.scaleSequential(d3.interpolateViridis)
      //   .domain([0, Math.log(d3.max(this.geoData.features, d => d.properties.population))])
      //   .interpolator(d3.interpolateBlues);

      this.svg.selectAll('path')
        .data(this.geoData.features)
        .enter()
        .append('path')
        .attr('d', this.geoPath)
        .attr('fill', d => this.fillColorFunction(d))
        .attr('stroke', '#000000');
      // // 绘制svg
      // this.svg.selectAll('path')
      //   .data(this.geoData.features)
      //   .enter()
      //   .append('path')
      //   .attr('d', this.geoPath)
      //   .attr('fill', d => colorScale(Math.log(d.properties.population)))
      //   .attr('stroke', '#000000');
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

    // //encoding Size
    // drawPopulationSquares() {
    //   const populationExtent = d3.extent(this.geoData.features, d => d.properties.population);
    //   const sizeScale = d3.scaleSqrt()
    //     .domain(populationExtent)
    //     .range([5, 50]); // 方块大小的范围

    //   // 直接在现有的SVG上绘制方块，不清除之前的内容
    //   this.geoData.features.forEach(feature => {
    //     const [x, y] = this.geoPath.centroid(feature);
    //     const population = feature.properties.population;
    //     this.svg.append('rect')
    //       .attr('x', x - sizeScale(population) / 2)
    //       .attr('y', y - sizeScale(population) / 2)
    //       .attr('width', sizeScale(population))
    //       .attr('height', sizeScale(population))
    //       .attr('fill', 'rgba(118, 139, 193, 0.7)');
    //   });
    // },

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
      console.log("Encoding Channel:", type);
      // 清除现有的 SVG 内容
      this.svg.selectAll('*').remove();

      if (type === this.myType['Color (Luminance)']) {
        // 应用蓝色编码
        const colorScale = d3.scaleSequential(d3.interpolateBlues)
          .domain([0, Math.log(d3.max(this.geoData.features, d => d.properties.population))]);

        // 重新绘制地图并应用颜色编码
        this.svg.selectAll('path')
          .data(this.geoData.features)
          .enter()
          .append('path')
          .attr('d', this.geoPath)
          .attr('fill', d => colorScale(Math.log(d.properties.population)))
          .attr('stroke', '#000000');
      }
      //Encoding Size
      else if (type === this.myType['Size']) {
        // 绘制地图的基本轮廓，不包含颜色编码或人口方块
        this.drawSvg();
        // 在地图上绘制人口方块
        // this.drawPopulationSquares();
        const populationExtent = d3.extent(this.geoData.features, d => d.properties.population);
        const sizeScale = d3.scaleSqrt()
          .domain(populationExtent)
          .range([5, 50]); // 方块大小的范围

        // 直接在现有的SVG上绘制方块，不清除之前的内容
        this.geoData.features.forEach(feature => {
          const [x, y] = this.geoPath.centroid(feature);
          const population = feature.properties.population;
          this.svg.append('rect')
            .attr('x', x - sizeScale(population) / 2)
            .attr('y', y - sizeScale(population) / 2)
            .attr('width', sizeScale(population))
            .attr('height', sizeScale(population))
            .attr('fill', 'rgba(118, 139, 193, 1)');
        });
      }
      //Encoding Quantity
      else if (type === this.myType['Quantity']) {
        this.drawSvg(); // 绘制地图的基本轮廓
        // 在地图上叠加人口方块
        const blockSize = 5; // 方块的边长
        const blockGap = 3; // 方块间的间隔
        const rowGap = 5; // 新增：行间距
        const populationPerBlock = 10000000; // 每个方块代表的人口数量

        // 直接在现有的SVG上绘制方块，不清除之前的内容
        this.geoData.features.forEach(feature => {
          const center = this.geoPath.centroid(feature);
          const population = feature.properties.population;
          const totalBlocks = Math.ceil(population / populationPerBlock); // 总方块数
          let blocksDrawn = 0; // 已绘制的方块数

          for (let row = 1; blocksDrawn < totalBlocks; row++) {
            for (let i = 0; i < row && blocksDrawn < totalBlocks; i++) {
              // 对x坐标的计算不变
              const x = center[0] - (blockSize + blockGap) * (row - 1) / 2 + (blockSize + blockGap) * i;
              // 调整y坐标的计算，以增加行间距
              const y = center[1] + ((blockSize + rowGap) * (row - 1)) - (row * blockSize / 2);
              this.svg.append('rect')
                .attr('x', x)
                .attr('y', y)
                .attr('width', blockSize)
                .attr('height', blockSize)
                .attr('fill', 'rgba(118, 139, 193, 1)'); // 方块的颜色
              blocksDrawn++;
            }
          }
        });
      }

      else {
        // 默认情况下使用单一的灰色，并绘制地图的基本轮廓
        this.drawSvg();
      }
    },


  },
}
</script>