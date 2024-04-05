<template>
    <div style="display: flex; height: 100%; width: 100%;">
        <v-card elevation="2" height="100%" width="35%" ref="selectorCard">
            <v-container style="display: flex; overflow-y: auto;" :id="value + '-seContainer'">
                <v-expansion-panels>
                    <v-expansion-panel>
                        <v-expansion-panel-title>
                            Basic Map Representations
                        </v-expansion-panel-title>

                        <v-expansion-panel-text>
                            <v-container class="container">
                                <v-row>
                                    <v-col class="element" @click="setRepresentation(myType['Political Map'])">
                                        Political Map
                                        <v-img :src="require('../assets/PoliticalMap.svg')" contain />
                                    </v-col>

                                    <v-col class="element" @click="setRepresentation(myType['Topographic Map'])">
                                        Topographic Map
                                        <v-img :src="require('../assets/TopographicMap.svg')" contain />
                                    </v-col>
                                </v-row>

                                <v-row>
                                    <v-col class="element" @click="setRepresentation(myType['Shape-based Map'])">
                                        Shape-based Map
                                        <v-img :src="require('../assets/Shape-basedMap.svg')" contain />
                                    </v-col>

                                    <v-col class="element" @click="setRepresentation(myType['Street Map'])">
                                        Street Map
                                        <v-img :src="require('../assets/StreetMap.svg')" contain />
                                    </v-col>
                                </v-row>

                                <v-row>
                                    <v-col class="element" @click="setRepresentation(myType['Grid Cartogram'])">
                                        Grid Cartogram
                                        <v-img :src="require('../assets/GridCartogram.svg')" contain />
                                    </v-col>

                                    <v-col></v-col>
                                </v-row>
                            </v-container>
                        </v-expansion-panel-text>
                    </v-expansion-panel>

                    <v-expansion-panel>
                        <v-expansion-panel-title>
                            Map Projections
                        </v-expansion-panel-title>

                        <v-expansion-panel-text>
                            <v-container class="container">
                                <v-row>
                                    <v-col class="element" @click="setProjection(myType['Mercator'])">
                                        Mercator
                                        <v-img :src="require('../assets/mercator.svg')" contain />
                                    </v-col>

                                    <v-col class="element" @click="setProjection(myType['Equirectangular'])">
                                        Equirectangular
                                        <v-img :src="require('../assets/equirectangular.svg')" contain />
                                    </v-col>
                                </v-row>
                            </v-container>
                        </v-expansion-panel-text>
                    </v-expansion-panel>

                    <v-expansion-panel>
                        <v-expansion-panel-title>
                            Encoding Channels
                        </v-expansion-panel-title>

                        <v-expansion-panel-text>
                            <v-container class="container">
                                <v-row>
                                    <v-col class="element" @click="setEncodingChannel(myType['Color (Luminance)'])">
                                        Color (Luminance)
                                        <v-img :src="require('../assets/Color(Luminance).svg')" contain />
                                    </v-col>

                                    <v-col class="element" @click="setEncodingChannel(myType['Color (Hue)'])">
                                        Color (Hue)
                                        <v-img :src="require('../assets/Color(Hue).svg')" contain />
                                    </v-col>
                                </v-row>

                                <v-row>
                                    <v-col class="element" @click="setEncodingChannel(myType['3D Length'])">
                                        3D Length
                                        <v-img :src="require('../assets/3DLength.svg')" contain />
                                    </v-col>

                                    <v-col class="element" @click="setEncodingChannel(myType['Glyph'])">
                                        Glyph
                                        <v-img :src="require('../assets/Glyph.svg')" contain />
                                    </v-col>
                                </v-row>

                                <v-row>
                                    <v-col class="element" @click="setEncodingChannel(myType['Link (Line)'])">
                                        Link (Line)
                                        <v-img :src="require('../assets/Link(Line).svg')" contain />
                                    </v-col>

                                    <v-col class="element" @click="setEncodingChannel(myType['Link (Arrow)'])">
                                        Link (Arrow)
                                        <v-img :src="require('../assets/Link(Arrow).svg')" contain />
                                    </v-col>
                                </v-row>

                                <v-row>
                                    <v-col class="element" @click="setEncodingChannel(myType['Size'])">
                                        Size
                                        <v-img :src="require('../assets/Size.svg')" contain />
                                    </v-col>

                                    <v-col class="element" @click="setEncodingChannel(myType['Quantity'])">
                                        Quantity
                                        <v-img :src="require('../assets/Quantity.svg')" contain />
                                    </v-col>
                                </v-row>
                            </v-container>
                        </v-expansion-panel-text>
                    </v-expansion-panel>
                    <v-expansion-panel>
                        <v-expansion-panel-title>
                            Highlight Techniques
                        </v-expansion-panel-title>

                        <v-expansion-panel-text>
                            <v-container class="container">
                                <v-row>
                                    <v-col class="element" @click="setHighlight(myType['Light'])">
                                        Light
                                        <v-img :src="require('../assets/HighlightLight.svg')" contain />
                                    </v-col>

                                    <v-col class="element" @click="setHighlight(myType['Color'])">
                                        Color
                                        <v-img :src="require('../assets/HighlightColor.svg')" contain />
                                    </v-col>
                                </v-row>

                                <v-row>
                                    <v-col class="element" @click="setHighlight(myType['Map Pin'])">
                                        Map Pin
                                        <v-img :src="require('../assets/HighlightMappin.svg')" contain />
                                    </v-col>

                                    <v-col class="element" @click="setHighlight(myType['3D Transformation'])">
                                        3D Transformation
                                        <v-img :src="require('../assets/Highlight3d.svg')" contain />
                                    </v-col>
                                </v-row>

                                <v-row>
                                    <v-col class="element" @click="setHighlight(myType['Enlarged Portions'])">
                                        Enlarged Portions
                                        <v-img :src="require('../assets/HighlightEnlarge.svg')" width="61%" contain />
                                    </v-col>
                                </v-row>
                            </v-container>
                        </v-expansion-panel-text>
                    </v-expansion-panel>



                    <v-expansion-panel>
                        <v-expansion-panel-title>
                            Label Positions
                        </v-expansion-panel-title>

                        <v-expansion-panel-text>
                            <v-container class="container">
                                <div class="sub-title" id="sub-title-0">Situated</div>
                                <v-container class="sub-container">
                                    <v-row>
                                        <v-col class="element" @click="setLabelPosition(myType['Label Situated'])">
                                            Situated
                                            <v-img :src="require('../assets/Situated.svg')" contain />
                                        </v-col>

                                        <v-col></v-col>
                                    </v-row>
                                </v-container>

                                <div class="sub-title">Matched</div>
                                <v-container class="sub-container">
                                    <v-row>
                                        <v-col class="element" @click="setLabelPosition(myType['Label Text'])">
                                            Text
                                            <v-img :src="require('../assets/MatchedText.svg')" contain />
                                        </v-col>

                                        <v-col class="element" @click="setLabelPosition(myType['Label Icon'])">
                                            Icon
                                            <v-img :src="require('../assets/MatchedIcon.svg')" contain />
                                        </v-col>
                                    </v-row>

                                    <v-row>
                                        <v-col class="element" @click="setLabelPosition(myType['Label Color'])">
                                            Color
                                            <v-img :src="require('../assets/MathchedColor.svg')" contain />
                                        </v-col>
                                        <v-col></v-col>
                                    </v-row>
                                </v-container>

                                <div class="sub-title">Linked</div>
                                <v-container class="sub-container">
                                    <v-row>
                                        <v-col style="padding: 0;">
                                            <v-col class="element"
                                                @click="setLabelPosition(myType['Label Convenient'])">
                                                Convenient
                                                <v-img :src="require('../assets/LinkedConvenient.svg')" contain />
                                            </v-col>

                                            <v-col class="element" @click="setLabelPosition(myType['Label Aligned'])">
                                                Aligned
                                                <v-img :src="require('../assets/LinkedAligned.svg')" contain />
                                            </v-col>

                                        </v-col>

                                        <v-col class="element" @click="setLabelPosition(myType['Label Ordered'])">
                                            Ordered
                                            <v-img :src="require('../assets/LinkedOrdered.svg')" contain />
                                        </v-col>
                                    </v-row>
                                </v-container>
                            </v-container>
                        </v-expansion-panel-text>
                    </v-expansion-panel>



                </v-expansion-panels>
            </v-container>
        </v-card>

        <v-container style="width: 100%; height: 100%; margin-left: 0; margin-right: 0" :ref="'d3Panel'">
            <svg :class="value + '-svg'" style="width: 100%; height: 100%;"></svg>
            <svg :class="value + '-legend'"
                style="position: absolute; top: 30px; right: 20px; width: 200px; height: 40px; z-index: 2;"></svg>
            <svg id="enlargedView"
                style="width: 200px; height: 200px; position: absolute; top: 10px; right: 10px;"></svg>
        </v-container>
    </div>
</template>

<script>
import * as d3 from 'd3';

export default {
    name: 'instanceTab',

    props: {
        geoData: {
            type: Object,
            required: true
        },

        infoData: {
            type: Object,
            required: true
        },

        value: {
            type: String,
            required: true
        },

        isNumerical: {
            type: Boolean,
            required: true
        }
    },

    data: () => ({
        representationType: 0,
        projectionType: 0,
        labelPositionType: -1,
        encodingChannelType: -1,
        highLightType: -1,

        svg: null,
        legend: null,

        mapWidth: 1000,
        mapHeight: 800,

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
            "Enlarged Portions": 4,

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

        },
    }),

    mounted() {
        console.log(this.value, "created, numerical:", this.isNumerical);
        
        let worldPopulation = 0;
        if (this.geoData && this.geoData.features && this.infoData) {
            this.geoData.features.forEach(feature => {
                worldPopulation += this.getPopulation(feature.properties.NAME);
            });
        }
        this.worldPopulation = worldPopulation;

        const cardEl = this.$refs.selectorCard.$el;

        this.$nextTick(() => {
            const height = cardEl.clientHeight;

            const seContainer = document.getElementById(this.value + '-seContainer');
            seContainer.style.maxHeight = (0.99 * height) + "px";

            this.initMap();
        });
    },

    methods: {
        initMap() {
            // 获得html中的地图（svg）标签
            this.svg = d3.select("." + this.value + "-svg");
            this.legend = d3.select("." + this.value + "-legend");

            //根据窗口大小设置地图的大小
            this.mapWidth = this.svg.node().getBoundingClientRect().width;
            this.mapHeight = this.svg.node().getBoundingClientRect().height;

            // console.log(this.mapWidth, this.mapHeight);
            this.setProjection(0);
            this.drawSvg();
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

        getPopulation(name) {
            // console.log(name, this.infoData[name]);
            return this.infoData[name] ? this.infoData[name] : -1
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
                const countryPopulation = this.getPopulation(feature.properties.NAME);
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

        // 设置 Map Representation
        setRepresentation(type) {
            console.log("Representation:", type)

            if (type === this.myType['Political Map']) {
                this.representationType = type;
                this.drawSvg();
            }
            else if (type === this.myType['Topographic Map']) {
                this.representationType = type;
            }
            else if (type === this.myType['Shape-based Map']) {
                this.representationType = type;

                // 移除现有的地图路径，准备绘制点阵地图
                this.svg.selectAll('path').remove();

                // 为地图上的每个国家绘制点阵图
                this.geoData.features.forEach(feature => {
                    // 计算每个国家边界框内网格的行数和列数
                    const bounds = d3.geoBounds(feature);
                    const [left, bottom] = this.geoProjection(bounds[0]);
                    const [right, top] = this.geoProjection(bounds[1]);
                    const w = right - left;
                    const h = bottom - top;
                    const rows = Math.ceil(h / 15); // 假设每20像素一个点的行距
                    const columns = Math.ceil(w / 15); // 假设每20像素一个点的列距
                    const pointRadius = 3; // 点的半径大小

                    // 生成特定国家边界框内的点
                    const points = [];
                    for (let i = 0; i < rows; i++) {
                        for (let j = 0; j < columns; j++) {
                            const x = left + j * (w / columns);
                            const y = top + i * (h / rows);
                            const point = this.geoProjection.invert([x, y]);
                            if (d3.geoContains(feature, point)) {
                                points.push({ x: x, y: y });
                            }
                        }
                    }

                    // 绘制点
                    this.svg.append("g")
                        .attr("fill", "black")
                        .attr("fill-opacity", 0.6)
                        .attr("stroke", "#fff")
                        .attr("stroke-width", 0.5)
                        .selectAll("circle")
                        .data(points)
                        .join("circle")
                        .attr("cx", d => d.x)
                        .attr("cy", d => d.y)
                        .attr("r", pointRadius);
                });
            }

            else if (type === this.myType['Street Map']) {
                this.representationType = type;
            }
            else if (type === this.myType['Grid Cartogram']) {
                this.representationType = type;

                // 首先，移除旧的网格层和旧的clipPath（如果存在）
                this.svg.select('.grid-layer').remove();
                this.svg.select('defs').selectAll('clipPath').remove(); // 假设没有其他clipPath在使用

                // 创建一个新的clipPath用于地图的轮廓
                const defs = this.svg.append('defs');
                defs.append('clipPath')
                    .attr('id', 'clip-map')
                    .append('path')
                    .datum(this.geoData)
                    .attr('d', this.geoPath);

                // 设置网格大小
                const gridSize = 30;

                // 创建网格层并应用clipPath
                const gridLayer = this.svg.append('g')
                    .classed('grid-layer', true)
                    .attr('clip-path', 'url(#clip-map)');

                // 计算网格线数量
                const numVerticalGrids = Math.ceil(this.mapWidth / gridSize);
                const numHorizontalGrids = Math.ceil(this.mapHeight / gridSize);

                // 绘制垂直网格线
                for (let i = 0; i < numVerticalGrids; i++) {
                    gridLayer.append('line')
                        .attr('x1', i * gridSize)
                        .attr('x2', i * gridSize)
                        .attr('y1', 0)
                        .attr('y2', this.mapHeight)
                        .style('stroke', 'black')
                        .style('stroke-opacity', 0.3);
                }

                // 绘制水平网格线
                for (let i = 0; i < numHorizontalGrids; i++) {
                    gridLayer.append('line')
                        .attr('y1', i * gridSize)
                        .attr('y2', i * gridSize)
                        .attr('x1', 0)
                        .attr('x2', this.mapWidth)
                        .style('stroke', 'black')
                        .style('stroke-opacity', 0.3);
                }
            }



        },

        // 设置 Map Projection
        setProjection(type) {
            console.log("Map Projection:", type);

            if (type === this.myType['Mercator']) {
                this.projectionType = type;

                this.geoProjection = d3.geoMercator()
                    .fitSize([this.mapWidth, this.mapHeight], this.geoData);
            }

            else if (type === this.myType['Equirectangular']) {
                this.projectionType = type;

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
            // this.svg.on('click', null);
            // d3.select("#enlargedView").selectAll("*").remove(); 
            // 根据类型应用新的高亮方式
            if (type === this.myType['Color']) {
                this.highLightType = type;

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
                this.highLightType = type;

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
                this.highLightType = type;

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
            else if (type === this.myType['3D Transformation']) {
                this.highLightType = type;

                const addHighLight = (event, svg) => {
                    // eslint-disable-next-line no-unused-vars
                    const [x, y] = d3.pointer(event, svg);
                    const feature = d3.select(event.target).datum(); // 获取被点击的地图区域的数据

                    // 高亮函数
                    const highLight = () => {
                        // 首先移除之前的高亮效果
                        //this.svg.selectAll('.highlight-3d-effect').remove();

                        // 然后添加一个新的具有3D效果的path
                        this.svg.append('path')
                            .datum(feature) // 使用同一区域的数据
                            .attr('class', 'highlight-3d-effect') // 为了方便之后可能的移除
                            .attr('d', this.geoPath) // 使用geoPath来保持地理形状的一致性
                            .attr('fill', 'rgba(33, 68, 158, 0.5)') // 为了简化，这里使用纯色填充表示阴影
                            .attr('filter', 'url(#drop-shadow)'); // 应用下面定义的SVG滤镜实现阴影效果

                        // 添加或确保SVG滤镜的存在
                        const defs = this.svg.append('defs');

                        const filter = defs.append('filter')
                            .attr('id', 'drop-shadow')
                            .attr('height', '130%');

                        filter.append('feGaussianBlur')
                            .attr('in', 'SourceAlpha')
                            .attr('stdDeviation', 3)
                            .attr('result', 'blur');

                        filter.append('feOffset')
                            .attr('in', 'blur')
                            .attr('dx', 5)
                            .attr('dy', 5)
                            .attr('result', 'offsetBlur');

                        const feMerge = filter.append('feMerge');
                        feMerge.append('feMergeNode')
                            .attr('in', 'offsetBlur');
                        feMerge.append('feMergeNode')
                            .attr('in', 'SourceGraphic');
                    };

                    highLight();
                    this.highLights.push(highLight);
                };

                // 绑定点击事件到所有的path上
                this.svg.selectAll('path').on('click', function (event) {
                    addHighLight(event, this);
                });
            }
            else if (type === this.myType['Enlarged Portions']) {
                this.highLightType = type;

                // 移除之前可能绑定的点击事件以避免重复
                this.svg.on('click', null);

                // 直接在点击事件中实现放大效果的逻辑
                this.svg.on('click', (event) => {
                    // 移除上一次点击留下的圆圈
                    this.svg.selectAll('circle.click-circle').remove();

                    const [x, y] = d3.pointer(event, this.svg.node());

                    // 在点击位置绘制一个圆圈作为反馈
                    this.svg.append('circle')
                        .classed('click-circle', true) // 添加一个类以便后续可以选择并移除
                        .attr('cx', x)
                        .attr('cy', y)
                        .attr('r', 30) // 圆的半径
                        .style('fill', 'none')
                        .style('stroke', 'red')
                        .style('stroke-width', 2);

                    // 清除#enlargedView中的内容
                    const enlargedView = d3.select('#enlargedView');
                    enlargedView.selectAll('*').remove();

                    // 在#enlargedView中创建一个新的svg元素
                    const enlargedViewSvg = enlargedView.append('svg')
                        .attr('width', '100%')
                        .attr('height', '100%')
                        .attr('viewBox', `${x - 30} ${y - 30} 60 60`);

                    // 创建圆形裁剪路径
                    const defs = enlargedViewSvg.append('defs');
                    const clipPath = defs.append('clipPath')
                        .attr('id', 'circle-clip');
                    clipPath.append('circle')
                        .attr('cx', x)
                        .attr('cy', y)
                        .attr('r', 30);

                    // 复制原SVG内容到新的SVG元素中，并应用圆形裁剪路径
                    enlargedViewSvg.append('g')
                        .attr('clip-path', 'url(#circle-clip)')
                        .html(this.svg.html());

                    // 由于SVG元素被复制，我们需要重新计算transform属性以确保放大的区域正确对齐
                    enlargedViewSvg.selectAll('g > svg')
                        .attr('x', null)
                        .attr('y', null)
                        .style('transform', `translate(${-x + 100}px, ${-y + 100}px) scale(2)`);
                });
            }



            // else if (type === this.myType['Enlarged Portions']) {
            //     this.highLightType = type;

            //     // 移除之前可能绑定的点击事件以避免重复
            //     this.svg.on('click', null);

            //     // 直接在点击事件中实现放大效果的逻辑
            //     this.svg.on('click', (event) => {
            //         const [x, y] = d3.pointer(event, this.svg.node());

            //         // 在点击位置绘制一个圆圈作为反馈
            //         this.svg.append('circle')
            //             .attr('cx', x)
            //             .attr('cy', y)
            //             .attr('r', 30) // 圆的半径
            //             .style('fill', 'none')
            //             .style('stroke', 'red')
            //             .style('stroke-width', 2);

            //         // 准备在#enlargedView中显示放大的内容
            //         const enlargedViewSvg = d3.select('#enlargedView').append('svg')
            //             .attr('width', 200)
            //             .attr('height', 200)
            //             .style('overflow', 'visible');

            //         // 计算viewBox的值来只显示点击点附近的区域
            //         // 注意：这里的30和2分别对应于圆的半径和期望的放大倍数
            //         const viewBoxX = x - 30;
            //         const viewBoxY = y - 30;
            //         const viewBoxWidth = 60; // 圆的直径
            //         const viewBoxHeight = 60; // 圆的直径

            //         enlargedViewSvg.attr('viewBox', `${viewBoxX} ${viewBoxY} ${viewBoxWidth} ${viewBoxHeight}`);

            //         // 复制原SVG内容到新的SVG元素中
            //         const content = this.svg.html();
            //         enlargedViewSvg.html(content);
            //     });
            // }









            // 添加更多的条件分支来处理其他类型的高亮方式
        },

        setLabelPosition(type) {
            console.log("Label Position:", type)
            if (type === this.myType['Label Situated']) {
                this.labelPositionType = type;
            }
            else if (type === this.myType['Label Text']) {
                this.labelPositionType = type;
            }
            else if (type === this.myType['Label Icon']) {
                this.labelPositionType = type;
            }
            else if (type === this.myType['Label Color']) {
                this.labelPositionType = type;
            }
            else if (type === this.myType['Label Convenient']) {
                this.labelPositionType = type;
            }
            else if (type === this.myType['Label Aligned']) {
                this.labelPositionType = type;
            }
            else if (type === this.myType['Label Ordered']) {
                this.labelPositionType = type;
            }
        },

        setEncodingChannel(type) {
            console.log("Encoding Channel:", type);

            //Encoding Color (Luminance)'
            if (type === this.myType['Color (Luminance)']) {
                this.encodingChannelType = type;

                // 重写encodingChannel函数
                this.encodingChannel = () => {
                    // 修改颜色映射的方法
                    const colorFunction = (scale) => {
                        const transformFunction = (input) => Math.pow(input, 0.25)
                        const colorScale = d3.scaleSequential(d3.interpolateBlues)
                            .domain([0, transformFunction(d3.max(this.geoData.features, d => this.getPopulation(d.properties.NAME)))]);
                        return scale == -1 ? this.defaultColor : colorScale(transformFunction(scale));
                    }

                    this.svg.selectAll('path')
                        .attr('fill', d => colorFunction(this.getPopulation(d.properties.NAME)));

                    this.drawLegend();
                }
            }

            //Encoding Color (Hue)'
            else if (type === this.myType['Color (Hue)']) {
                this.encodingChannelType = type;

                // 重写encodingChannel函数
                this.encodingChannel = () => {
                    // 修改颜色映射的方法
                    const colorFunction = (population) => {
                        if (population < 0) {
                            return this.defaultColor;
                        }
                        else if (population >= 0 && population < 5000000) {
                            return 'blue'; // 人口数量小于5000000
                        } else if (population >= 5000000 && population < 10000000) {
                            return 'green'; // 人口数量在5000000-10000000之间
                        } else if (population >= 10000000 && population < 50000000) {
                            return 'yellow'; // 人口数量在10000000-50000000之间
                        } else if (population >= 50000000 && population < 100000000) {
                            return 'orange'; // 人口数量在50000000-100000000之间
                        } else {
                            return 'red'; // 人口数量大于100000000
                        }
                    };

                    this.svg.selectAll('path')
                        .attr('fill', d => colorFunction(this.getPopulation(d.properties.NAME)));
                };
            }


            //Encoding 3D Length
            else if (type === this.myType['3D Length']) {
                this.encodingChannelType = type;

                this.encodingChannel = () => {
                    // 在地图上绘制模拟的3D长方体
                    const baseHeight = 3; // 长方体基础高度，所有长方体至少有这个高度
                    const populationPerHeight = 800000; // 每增加这么多人口，长方体的高度增加一单位
                    const cuboidWidth = 20; // 长方体的宽度
                    const cuboidLength = 30; // 长方体的长度（在SVG中模拟的“深度”）
                    const sideOpacity = 0.5; // 侧面的不透明度

                    this.geoData.features.forEach(feature => {
                        const center = this.geoPath.centroid(feature);
                        const population = this.getPopulation(feature.properties.NAME);
                        if (population >= 1000000) { // 人口大于等于1000000时绘制长方体
                            const height = baseHeight + (population / populationPerHeight); // 长方体的总高度

                            // 绘制长方体的“前面”
                            this.svg.append('rect')
                                .attr('x', center[0] - cuboidWidth / 2)
                                .attr('y', center[1] - height)
                                .attr('width', cuboidWidth)
                                .attr('height', height)
                                .attr('fill', 'rgba(125, 125, 255, 0.7)'); // 修改前面的颜色

                            // 绘制长方体的“顶面”
                            this.svg.append('polygon')
                                .attr('points', `${center[0] - cuboidWidth / 2},${center[1] - height} ${center[0] + cuboidWidth / 2},${center[1] - height} ${center[0] + cuboidWidth / 2 - cuboidLength / 4},${center[1] - height - cuboidLength / 4} ${center[0] - cuboidWidth / 2 - cuboidLength / 4},${center[1] - height - cuboidLength / 4}`)
                                .attr('fill', 'rgba(150, 150, 255, 0.7)');

                            // 绘制长方体的“左侧面”
                            this.svg.append('polygon')
                                .attr('points', `${center[0] - cuboidWidth / 2},${center[1]} ${center[0] - cuboidWidth / 2},${center[1] - height} ${center[0] - cuboidWidth / 2 - cuboidLength / 4},${center[1] - height - cuboidLength / 4} ${center[0] - cuboidWidth / 2 - cuboidLength / 4},${center[1] - cuboidLength / 4}`)
                                .attr('fill', `rgba(75, 75, 255, ${sideOpacity})`); // 修改左侧面的颜色
                        }
                    });
                }
            }


            else if (type === this.myType['Glyph']) {
                this.encodingChannelType = type;

                this.encodingChannel = () => {
                    this.drawPieCharts(); // 在地图上叠加饼状图
                }
            }

            // Encoding Size
            else if (type === this.myType['Size']) {
                this.encodingChannelType = type;

                this.encodingChannel = () => {
                    // 在地图上绘制人口方块
                    // this.drawPopulationSquares();
                    const populationExtent = d3.extent(this.geoData.features, d => this.getPopulation(d.properties.NAME));
                    const sizeScale = d3.scaleSqrt()
                        .domain(populationExtent)
                        .range([5, 50]); // 方块大小的范围

                    // 直接在现有的SVG上绘制方块，不清除之前的内容
                    this.geoData.features.forEach(feature => {
                        const [x, y] = this.geoPath.centroid(feature);
                        const population = this.getPopulation(feature.properties.NAME);
                        if (population >= 1000000) { // 人口大于等于1000000时绘制方块
                            this.svg.append('rect')
                                .attr('x', x - sizeScale(population) / 2)
                                .attr('y', y - sizeScale(population) / 2)
                                .attr('width', sizeScale(population))
                                .attr('height', sizeScale(population))
                                .attr('fill', 'rgba(118, 139, 193, 1)');
                        }
                    });
                }
            }


            //Encoding Quantity
            else if (type === this.myType['Quantity']) {
                this.encodingChannelType = type;

                this.encodingChannel = () => {
                    // 在地图上叠加人口图标
                    const iconWidth = 6; // 图标的宽度
                    const iconHeight = 15; // 图标的高度
                    const iconGap = 1; // 调整图标间的间隔

                    // 直接在现有的SVG上绘制图标，不清除之前的内容
                    this.geoData.features.forEach(feature => {
                        const center = this.geoPath.centroid(feature);
                        const population = this.getPopulation(feature.properties.NAME);

                        // 只有当人口大于等于1000000时才绘制图标
                        if (population >= 1000000) {
                            const totalIcons = Math.ceil(population / 8000000); // 总图标数

                            for (let i = 0; i < totalIcons; i++) {
                                // 计算图标的位置
                                // 将图标排列成一行显示5个图标的形式
                                const x = center[0] - ((iconWidth + iconGap) * 5 / 2) + ((i % 5) * (iconWidth + iconGap));
                                const y = center[1] + (Math.floor(i / 5) * (iconHeight + iconGap));
                                // 添加图标
                                this.svg.append('image')
                                    .attr('xlink:href', require('../assets/PersonIcon.svg')) // 图标的路径
                                    .attr('x', x)
                                    .attr('y', y)
                                    .attr('width', iconWidth)
                                    .attr('height', iconHeight);
                            }
                        }
                    });
                }
            }

            else {
                this.encodingChannelType = -1;

                // 默认情况下使用单一的灰色，并绘制地图的基本轮廓
                this.encodingChannel = () => {
                    this.svg.selectAll("path").attr("fill", this.defaultColor);
                }
            }

            this.drawSvg();
        },

        drawLegend() {
            const legendWidth = 200;
            const legendHeight = 20;

            const colorScale = d3.scaleSequential(d3.interpolateBlues)
                .domain([0, d3.max(this.geoData.features, d => this.getPopulation(d.properties.NAME))]);

            const legendGradient = this.legend.append('svg')
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
            this.legend.append('text')
                .attr('x', 0)
                .attr('y', legendHeight + 15)
                .text('0');

            // 添加最大值标签
            this.legend.append('text')
                .attr('x', legendWidth - 20)
                .attr('y', legendHeight + 15)
                .text(d3.max(this.geoData.features, d => this.getPopulation(d.properties.NAME)));
        },
    },

}
</script>

<style scoped>
.container {
    padding: 0px;
}

.sub-container {
    border: 1px dotted;
    border-color: #E1CBD8;
}

.sub-title {
    margin-top: 6px;
    padding: 3px;
    font-size: 14px;
    border-radius: 6px;
    display: block;
    width: fit-content;
    background-color: #E1CBD8;
}

#sub-title-0 {
    margin-top: 0px;
}

.element {
    background-color: white;
}

.element:hover {
    transform: scale(1.12);
    border: 0.67px solid;
    border-color: #E1CBD8;
}
</style>