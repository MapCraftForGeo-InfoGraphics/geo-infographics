<template>
  <v-container style="width: 100%; height: 100%; margin-left: 0; margin-right: 0">
    <svg ref="svg" style="width: 100%; height: 100%;"></svg>
    <svg class="legend"></svg>
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

    defaultColor: '#cccccc',

    encodingChannel: () => { },
    highLights: [],

    myType: {
      "Political Map": 0,
      "Topographic Map": 1,
      "Shape-based Map": 2,
      "Street Map": 3,
      "Grid Cartogram": 4,


      "Mercator": 0,
      "Equirectangular": 1,

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
    Promise.all([
      this.loadJson('countries.geojson'),
      this.loadJson('country-by-population.json')
    ])

      .then(([geoData, popuData]) => {
        this.geoData = geoData;
        this.popuData = popuData["data"];

        let worldPopulation = 0;
        if (this.geoData && this.geoData.features && this.popuData) {
          this.geoData.features.forEach(feature => {
            const populationInfo = this.popuData.find(item => item.country === feature.properties.ADMIN);
            const population = populationInfo ? populationInfo.population : 0;
            feature.properties.population = population;
            worldPopulation += population;
          });
        }
        this.worldPopulation = worldPopulation;

        // Now setProjection and initMap once data is fully prepared
        this.initMap();
      })

      .catch(error => {
        console.error('Error loading data:', error);
        // Handle loading errors
      });
  },

  methods: {
    initMap() {
      // 获得html中的地图（svg）标签
      this.svg = d3.select(this.$refs.svg);

      //根据窗口大小设置地图的大小
      this.mapWidth = this.svg.node().getBoundingClientRect().width;
      this.mapHeight = this.svg.node().getBoundingClientRect().height;

      this.setProjection(0);
    },

    //重新绘制svg
    drawSvg() {
      // 移除现有的 SVG
      this.svg.selectAll('*').remove();

      this.svg.selectAll('path')
        .data(this.geoData.features)
        .enter()
        .append('path')
        .attr('d', this.geoPath)
        .attr('stroke', '#ffffff')
        .attr("fill", this.defaultColor);

      this.encodingChannel();

      this.highLights.forEach(highLight => {
        highLight();
      });
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

    // 设置 Map Representation
    setRepresentation(type) {
      console.log("Representation:", type)
    },

    // 设置 Map Projection
    // 0: Mollweide
    // 1: Robinson
    setProjection(type) {
      console.log("Map Projection:", type);

      if (type === this.myType['Mercator']) {
        // this.geoProjection = d3.geoProjection(function (x, y) {
        //   var lambda = x / 180 * Math.PI;
        //   var phi = y / 180 * Math.PI;
        //   var theta = Math.asin((2 * phi) / Math.PI);
        //   var _x = (Math.sqrt(2) / Math.PI) * lambda * Math.cos(theta);
        //   var _y = Math.sqrt(2) / Math.PI * Math.sin(theta);
        //   return [_x, _y];
        // }).fitSize([this.mapWidth, this.mapHeight], this.geoData);
        this.geoProjection = d3.geoMercator()
          .fitSize([this.mapWidth, this.mapHeight], this.geoData);
      }

      else if (type === this.myType['Equirectangular']) {
        // this.geoProjection = d3.geoProjection(function (x, y) {
        //   // 投影函数
        //   var lambda = x / 180 * Math.PI;
        //   var phi = y / 180 * Math.PI;
        //   var phi_1 = Math.asin(2 / Math.PI * Math.sin(phi));
        //   var theta = 0.8 * lambda * Math.cos(phi_1);
        //   var _x = 2 / Math.PI * theta;
        //   var _y = Math.sin(phi_1);
        //   return [_x, _y];
        // }).fitSize([this.mapWidth, this.mapHeight], this.geoData);
        // this.geoProjection = d3.geoEquirectangular()
        this.geoProjection = d3.geoEquirectangular()
          .fitSize([this.mapWidth, this.mapHeight], this.geoData);
      }

      this.geoPath = d3.geoPath().projection(this.geoProjection);
      this.drawSvg();
    },


    setHighlight(type) {
      console.log("Highlight Techniques:", type);

      // 重置所有路径的填充颜色到默认颜色
      // this.svg.selectAll('path')
      //   .attr('fill', d => this.fillColorFunction(d.properties.populationd))
      //   .classed('highlighted', false); // 假设你使用了highlighted类来表示高亮

      // // 移除所有之前添加的特定高亮元素
      // this.svg.selectAll('.highlight-marker').remove();

      // 取消之前的所有点击事件监听器
      this.svg.selectAll('path').on('click', null);
      // 重要：移除绑定到SVG本身的点击事件监听器
      this.svg.on('click', null);

      // 根据类型应用新的高亮方式
      if (type === this.myType['Color']) {
        const addHighLight = (svg) => {
          const highLight = () => {
            console.log(svg);
            d3.select(svg)
              .classed('highlighted', true) // 使用类来标记高亮
              .attr('fill', 'red');
          };

          highLight(svg);
          this.highLights.push(highLight);
        };

        this.svg.selectAll('path')
          .on('click', function () { addHighLight(this) });
      }

      else if (type === this.myType['Light']) {
        const addHighLight = (event, svg) => {
          const [x, y] = d3.pointer(event, svg);

          const highLight = () => {
            // 添加一个SVG图标作为光圈效果
            d3.select(svg).append('image')
              .classed('highlight-marker', true) // 使用类来标记这是一个高亮标记
              .attr('xlink:href', require('../assets/lightIcon.svg'))// 设置图像的路径
              .attr('x', x - 40) // 调整图像位置，使其中心对准点击位置
              .attr('y', y - 40) // 同上，这里的15是假设图像大小为30x30像素，需要根据实际大小调整
              .attr('width', 80) // 设置图像的宽度
              .attr('height', 80); // 设置图像的高度
          };

          highLight();
          this.highLights.push(highLight);
        };

        // 绑定一个新的点击事件监听器到SVG本身
        this.svg.on('click', function (event) {
          addHighLight(event, this)
        });
      }

      else if (type === this.myType['Map Pin']) {
        const addHighLight = (event, svg) => {
          const [x, y] = d3.pointer(event, svg);

          const highLight = () => {
            // 添加一个SVG图标作为光圈效果
            d3.select(svg).append('image')
              .classed('highlight-marker', true) // 使用类来标记这是一个高亮标记
              .attr('xlink:href', require('../assets/locationIcon.png'))// 设置图像的路径
              .attr('x', x - 40) // 调整图像位置，使其中心对准点击位置
              .attr('y', y - 96) // 同上，这里的15是假设图像大小为30x30像素，需要根据实际大小调整
              .attr('width', 80) // 设置图像的宽度
              .attr('height', 96); // 设置图像的高度
          };

          highLight();
          this.highLights.push(highLight);
        };

        // 绑定一个新的点击事件监听器到SVG本身
        this.svg.on('click', function (event) {
          addHighLight(event, this);
        });
      }


      // 添加更多的条件分支来处理其他类型的高亮方式
    },

    setLabelPosition(type) {
      console.log("Label Position:", type)
    },

    //encoding glyph
    //contryPopulation/worldPopulation
    drawPieCharts() {
      const radius = 15; // 饼状图的半径，可根据需要调整大小

      const arcGenerator = d3.arc()
        .innerRadius(0) // 0表示这是个饼状图，而不是环状图
        .outerRadius(radius);

      const pieGenerator = d3.pie()
        .value(d => d.value)
        .sort(null); // 不对切片进行排序

      this.geoData.features.forEach(feature => {
        const countryPopulation = feature.properties.population;
        const populationPercentage = countryPopulation / this.worldPopulation;
        // const data = [{ value: populationPercentage }, { value: 1 - populationPercentage }]; // 饼状图数据
        const data = [
          { value: populationPercentage, isCountryPopulation: true },
          { value: 1 - populationPercentage, isCountryPopulation: false }
        ];

        const arcs = pieGenerator(data);

        const center = this.geoPath.centroid(feature);

        console.log(arcs); // To inspect the overall structure

        arcs.forEach(arc => {
          this.svg.append('path')
            .attr('d', arcGenerator(arc))
            .attr('transform', `translate(${center[0]}, ${center[1]})`)
            .attr('fill', function () {
              return arc.data.isCountryPopulation ? 'rgba(0, 100, 255, 0.7)' : 'rgba(200, 200, 200, 0.3)';
            });
        });
      });
    },

    setEncodingChannel(type) {
      console.log("Encoding Channel:", type);

      //Encoding Color (Luminance)'
      if (type === this.myType['Color (Luminance)']) {
        // 重写encodingChannel函数
        this.encodingChannel = () => {
          // 修改颜色映射的方法
          const colorFunction = (scale) => {
            const transformFunction = (input) => Math.pow(input, 0.25)
            const colorScale = d3.scaleSequential(d3.interpolateBlues)
              .domain([0, transformFunction(d3.max(this.geoData.features, d => d.properties.population))]);
            return colorScale(transformFunction(scale));
          }

          this.svg.selectAll('path')
            .attr('fill', d => colorFunction(d.properties.population));

          this.drawLegend();
        }
      }

      //Encoding Color (Hue)'
      else if (type === this.myType['Color (Hue)']) {
        // 重写encodingChannel函数
        this.encodingChannel = () => {
          //修改颜色映射的方法
          const colorFunction = (category) => {
            const transformFunction = (input) => Math.pow(input, 0.25)
            const colorScale = d3.scaleSequential(d3.interpolateYlGnBu)
              .domain([0, transformFunction(d3.max(this.geoData.features, d => d.properties.population))]);

            return colorScale(transformFunction(category));
          }

          this.svg.selectAll('path')
            .attr('fill', d => colorFunction(d.properties.population))
        }
      }

      //Encoding 3D Length
      else if (type === this.myType['3D Length']) {
        this.encodingChannel = () => {
          // 在地图上绘制模拟的3D长方体
          const baseHeight = 5; // 长方体基础高度，所有长方体至少有这个高度
          const populationPerHeight = 10000000; // 每增加这么多人口，长方体的高度增加一单位
          const cuboidWidth = 10; // 长方体的宽度
          const cuboidLength = 20; // 长方体的长度（在SVG中模拟的“深度”）
          const sideOpacity = 0.5; // 侧面的不透明度

          this.geoData.features.forEach(feature => {
            const center = this.geoPath.centroid(feature);
            const population = feature.properties.population;
            const height = baseHeight + (population / populationPerHeight); // 长方体的总高度

            // 绘制长方体的“前面”
            this.svg.append('rect')
              .attr('x', center[0] - cuboidWidth / 2)
              .attr('y', center[1] - height)
              .attr('width', cuboidWidth)
              .attr('height', height)
              .attr('fill', 'rgba(100, 100, 255, 0.7)');

            // 绘制长方体的“顶面”
            this.svg.append('polygon')
              .attr('points', `${center[0] - cuboidWidth / 2},${center[1] - height} ${center[0] + cuboidWidth / 2},${center[1] - height} ${center[0] + cuboidWidth / 2 - cuboidLength / 4},${center[1] - height - cuboidLength / 4} ${center[0] - cuboidWidth / 2 - cuboidLength / 4},${center[1] - height - cuboidLength / 4}`)
              .attr('fill', 'rgba(150, 150, 255, 0.7)');

            // 绘制长方体的“左侧面”
            this.svg.append('polygon')
              .attr('points', `${center[0] - cuboidWidth / 2},${center[1]} ${center[0] - cuboidWidth / 2},${center[1] - height} ${center[0] - cuboidWidth / 2 - cuboidLength / 4},${center[1] - height - cuboidLength / 4} ${center[0] - cuboidWidth / 2 - cuboidLength / 4},${center[1] - cuboidLength / 4}`)
              .attr('fill', `rgba(100, 100, 255, ${sideOpacity})`);
          });
        }
      }

      else if (type === this.myType['Glyph']) {
        this.encodingChannel = () => {
          this.drawPieCharts(); // 在地图上叠加饼状图
        }
      }

      //Encoding Size
      else if (type === this.myType['Size']) {
        this.encodingChannel = () => {
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

      }

      //Encoding Quantity
      else if (type === this.myType['Quantity']) {
        this.encodingChannel = () => {
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
      }

      else {
        // 默认情况下使用单一的灰色，并绘制地图的基本轮廓
        this.encodingChannel = () => {
          this.svg.selectAll("path").attr("fill", this.defaultColor);
        }
      }

      this.drawSvg();
    },

    drawLegend() {
      const legendContainer = d3.select('.legend');
      const legendWidth = 200;
      const legendHeight = 20;

      const colorScale = d3.scaleSequential(d3.interpolateBlues)
        .domain([0, d3.max(this.geoData.features, d => d.properties.population)]);

      const legendGradient = legendContainer.append('svg')
        .attr('width', legendWidth)
        .attr('height', legendHeight);

      // 创建渐变色彩
      const gradient = legendGradient.append('defs')
        .append('linearGradient')
        .attr('id', 'legendGradient')
        .attr('x1', '0%')
        .attr('y1', '0%')
        .attr('x2', '100%')
        .attr('y2', '0%');

      gradient.append('stop')
        .attr('offset', '0%')
        .attr('stop-color', colorScale.range()[0]);

      gradient.append('stop')
        .attr('offset', '100%')
        .attr('stop-color', colorScale.range()[1]);

      // 绘制渐变色块
      legendGradient.append('rect')
        .attr('width', legendWidth)
        .attr('height', legendHeight)
        .style('fill', 'url(#legendGradient)');

      // 添加最小值标签
      legendContainer.append('text')
        .attr('x', 0)
        .attr('y', legendHeight + 15)
        .text('0');

      // 添加最大值标签
      legendContainer.append('text')
        .attr('x', legendWidth - 20)
        .attr('y', legendHeight + 15)
        .text(d3.max(this.geoData.features, d => d.properties.population));
    },


  },
}
</script>

<style scoped>
.legend {
  position: absolute;
  top: 75px;
  right: 10px;
  width: 200px;
  height: 40px;
  z-index: 2; /* 将悬浮元素置于其他元素之上 */
}
</style>