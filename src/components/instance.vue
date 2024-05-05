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
                                    <v-col class="element" @click="setRepresentation(myType['Plain'])">
                                        <input type="button" id="myButtonPlain" class="colorfulButton"
                                           v-model=plainTextLabel @click="setRepresentation(myType['Plain'])"/>
                                    </v-col>
                                </v-row>
                                <v-row>
                                    <v-col class="element" @click="setRepresentation(myType['Political Map'])">
                                        Political Map
                                        <v-img :src="require('../assets/PoliticalMap.svg')" contain/>
                                    </v-col>

                                    <!-- <v-col class="element" @click="setRepresentation(myType['Topographic Map'])">
                                        Topographic Map
                                        <v-img :src="require('../assets/TopographicMap.svg')" contain />
                                    </v-col> -->
                                    <v-col class="element" @click="setRepresentation(myType['Shape-based Map'])">
                                        Shape-based Map
                                        <v-img :src="require('../assets/Shape-basedMap.svg')" contain/>
                                    </v-col>
                                </v-row>

                                <!-- <v-row>
                                    <v-col class="element" @click="setRepresentation(myType['Shape-based Map'])">
                                        Shape-based Map
                                        <v-img :src="require('../assets/Shape-basedMap.svg')" contain />
                                    </v-col>

                                    <v-col class="element" @click="setRepresentation(myType['Street Map'])">
                                        Street Map
                                        <v-img :src="require('../assets/StreetMap.svg')" contain />
                                    </v-col>
                                </v-row> -->

                                <v-row>
                                    

                                    <v-col class="element" @click="setRepresentation(myType['Terrain'])">
                                        Topographic Map
                                        <v-img :src="require('../assets/TerrainGlobal.svg')" contain/>
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
                                        <v-img :src="require('../assets/mercator.svg')" contain/>
                                    </v-col>

                                    <v-col class="element" @click="setProjection(myType['Equirectangular'])">
                                        Equirectangular
                                        <v-img :src="require('../assets/equirectangular.svg')" contain/>
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
                                    <v-col>
                                        <input type="button" id="myButton" class="colorfulButton"
                                               v-model=ifDoubleEncodingText @click="doubleEncoding()"/>
                                    </v-col>
                                    <v-col>
                                        <input type="button" id="myButtonRemove" class="colorfulButton"
                                               v-model=removeText @click="setEncodingChannel(myType['Remove'])"/>
                                    </v-col>

                                </v-row>

                                <v-row>
                                    <div class="row-with-line"></div>
                                    <v-col class="element" @click="setEncodingChannel(myType['Color (Luminance)'])">
                                        Color (Intensity)
                                        <v-img :src="require('../assets/Color(Luminance).svg')" contain/>
                                    </v-col>

                                    <v-col class="element" @click="setEncodingChannel(myType['Color (Hue)'])">
                                        Color (Hue)
                                        <v-img :src="require('../assets/Color(Hue).svg')" contain/>
                                    </v-col>
                                </v-row>

                                <v-row>
                                    <div class="row-with-line"></div>
                                    <v-col class="element" @click="setEncodingChannel(myType['3D Length'])">
                                        3D Length
                                        <v-img :src="require('../assets/3DLength.svg')" contain/>
                                    </v-col>

                                    <v-col class="element" @click="setEncodingChannel(myType['2D Length'])">
                                        2D Length
                                        <v-img :src="require('../assets/BarChart.svg')" contain/>
                                    </v-col>
                                </v-row>

                                <v-row>
                                    <div class="row-with-line"></div>
                                    <v-col class="element" @click="setEncodingChannel(myType['Quantity'])">
                                        Quantity
                                        <v-img :src="require('../assets/Quantity.svg')" contain/>
                                    </v-col>
                                    <v-col class="element" @click="setEncodingChannel(myType['Size'])">
                                        Size
                                        <v-img :src="require('../assets/Size.svg')" contain/>
                                    </v-col>
                                </v-row>

                                <v-row>
                                    <div class="row-with-line"></div>
                                    <v-col class="element" @click="setEncodingChannel(myType['Link (Line)'])">
                                        Tilt/Angle (Undirected)
                                        <v-img :src="require('../assets/Link(Line).svg')" contain/>
                                    </v-col>

                                    <v-col class="element" @click="setEncodingChannel(myType['Link (Arrow)'])">
                                        Tilt/Angle (Directed)
                                        <v-img :src="require('../assets/Link(Arrow).svg')" contain/>
                                    </v-col>
                                </v-row>

                                <v-row>
                                    <div class="row-with-line"></div>
                                    <v-col class="element" @click="setEncodingChannel(myType['Glyph'])">
                                        Glyph
                                        <v-img :src="require('../assets/Glyph.svg')" width="50%" contain/>
                                    </v-col>

                                    <!-- <v-col class="element" @click="setEncodingChannel(myType['Remove'])">
                                        Remove
                                        <v-img :src="require('../assets/Glyph.svg')" width="50%" contain />
                                    </v-col> -->
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
                                <v-row class="button-row">
                                    <input type="button" id="myButtonRemoveLabel" class="colorfulButton"
                                           v-model=removeTextLabel @click="setLabelPosition(myType['Label Remove'])"/>
                                </v-row>
                                <v-row>
                                    <v-col style="padding: 0;">
                                        <div class="matched-heading">Situated</div>
                                    </v-col>
                                </v-row>
                                <v-row>
                                    <div class="row-with-line"></div>
                                    <v-col class="element" @click="setLabelPosition(myType['Label Situated'])">
                                        Situated
                                        <v-img :src="require('../assets/Situated.svg')" contain/>
                                    </v-col>

                                    <v-col></v-col>
                                </v-row>

                                <v-row>
                                    <v-col style="padding: 0;">
                                        <div class="matched-heading">Matched</div>
                                    </v-col>
                                </v-row>
                                <v-row>
                                    <div class="row-with-line"></div>
                                    <v-col style="padding: 0;">
                                        <v-col class="element" @click="setLabelPosition(myType['Label Text'])">
                                            Text
                                            <v-img :src="require('../assets/MatchedText.svg')" contain/>
                                        </v-col>
                                        <v-col class="element" @click="setLabelPosition(myType['Label Color'])">
                                            Color
                                            <v-img :src="require('../assets/MathchedColor.svg')" contain/>
                                        </v-col>
                                    </v-col>
                                    <v-col class="element" @click="setLabelPosition(myType['Label Icon'])">
                                        Icon
                                        <v-img :src="require('../assets/MatchedIcon.svg')" contain/>
                                    </v-col>
                                </v-row>

                                <v-row>
                                    <v-col style="padding: 0;">
                                        <div class="matched-heading">Linked</div>
                                    </v-col>
                                </v-row>
                                <v-row>
                                    <div class="row-with-line"></div>
                                    <v-col style="padding: 0;">
                                        <v-col class="element"
                                               @click="setLabelPosition(myType['Label Convenient'])">
                                            Convenient
                                            <v-img :src="require('../assets/LinkedConvenient.svg')" contain/>
                                        </v-col>

                                        <v-col class="element" @click="setLabelPosition(myType['Label Aligned'])">
                                            Aligned
                                            <v-img :src="require('../assets/LinkedAligned.svg')" contain/>
                                        </v-col>

                                    </v-col>

                                    <v-col class="element" @click="setLabelPosition(myType['Label Ordered'])">
                                        Ordered
                                        <v-img :src="require('../assets/LinkedOrdered.svg')" contain/>
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
                                    <input type="button" id="myButtonRemoveHighlight" class="colorfulButton"
                                           v-model=removeTextHighlight
                                           @click="setHighlight(myType['Highlight Remove'])"/>
                                </v-row>
                                <v-row>
                                    <v-col class="element" @click="setHighlight(myType['Light'])">
                                        Light
                                        <v-img :src="require('../assets/HighlightLight.svg')" contain/>
                                    </v-col>

                                    <v-col class="element" @click="setHighlight(myType['Color'])">
                                        Color
                                        <v-img :src="require('../assets/HighlightColor.svg')" contain/>
                                    </v-col>
                                </v-row>

                                <v-row>
                                    <v-col class="element" @click="setHighlight(myType['Map Pin'])">
                                        Map Pin
                                        <v-img :src="require('../assets/HighlightMappin.svg')" contain/>
                                    </v-col>

                                    <v-col class="element" @click="setHighlight(myType['3D Transformation'])">
                                        3D Transformation
                                        <v-img :src="require('../assets/Highlight3d.svg')" contain/>
                                    </v-col>
                                </v-row>

                                <v-row>
                                    <v-col class="element" @click="setHighlight(myType['Enlarged Portions'])">
                                        Enlarged Portions
                                        <v-img :src="require('../assets/HighlightEnlarge.svg')" contain/>
                                    </v-col>
                                    <v-col class="element" @click="setHighlight(myType['Edge Stroke'])">
                                        Contour
                                        <v-img :src="require('../assets/HighlightEdgeStroking.svg')" contain/>
                                    </v-col>
                                </v-row>
                            </v-container>
                        </v-expansion-panel-text>
                    </v-expansion-panel>
                    <v-expansion-panel>
                        <v-expansion-panel-title>
                            Print
                        </v-expansion-panel-title>
                        <v-expansion-panel-text>
                            <v-container class="container">
                                <v-row>
                                    <input type="button" id="myButtonPrint" class="colorfulButton" v-model=printText
                                           @click="printSVG()"/>
                                </v-row>
                            </v-container>
                        </v-expansion-panel-text>

                    </v-expansion-panel>
                </v-expansion-panels>
            </v-container>
        </v-card>

        <v-container style="width: 100%; height: 100%; margin-left: 0; margin-right: 0" :ref="'d3Panel'">
            <v-row>
                <v-col ref="legendCol">
                    <svg :class="value + '-legend'" style="height: 40px; width: 100%;"></svg>
                </v-col>
                <v-col></v-col>
                <v-col></v-col>


            </v-row>
            <svg :class="value + '-svg'" style="width: 100%; height: 100%;"></svg>
            <!-- <svg :class="value + '-legend'" style="position: absolute; top: 30px; right: 20px; width: 200px; height: 40px; z-index: 2;"></svg> -->
            <svg :id="value + '-enlargedView'"
                 style="width: 200px; height: 400px; position: absolute; top: 10px; right: 10px;"></svg>
        </v-container>
    </div>

    <v-dialog v-model="errorDialog" width="auto">
        <v-card max-width="400" prepend-icon="mdi-alert-circle-outline" :title="errorTitle" :text="errorMessage">
            <template v-slot:actions>
                <v-btn class="ms-auto" text="Ok" @click="errorDialog = false"></v-btn>
            </template>
        </v-card>
    </v-dialog>
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

        propName: {
            type: String,
            required: false
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

        worldPopulation: 0,
        mostPopulation: 0,

        svg: null,
        legend: null,

        mapWidth: 1000,
        mapHeight: 800,

        legendWidth: 200,

        defaultColor: '#cccccc',

        errorTitle: '',
        errorMessage: '',
        errorDialog: false,

        ifDoubleEncoding: false,
        ifDoubleEncodingText: 'Dual Encoding: OFF',
        removeText: 'No Encoding',
        removeTextLabel: 'No Label',
        removeTextHighlight: 'No Highlight',
        plainTextLabel: 'No Map',
        preEncoding: -1,
        preColortype: -1,

        encodingChannel: () => {
        },
        representation: () => {
        },
        LabelPosition: () => {
        },

        colorFunctionL: () => {
        },

        highLights: [],
        pointer2highlight: 0,

        printText: 'Print',

        myType: {
            "Political Map": 0,
            "Topographic Map": 1,
            "Shape-based Map": 2,
            "Street Map": 3,
            "Plain": 4,
            "Terrain": 5,


            "Mercator": 0,
            "Equirectangular": 1,

            "Light": 0,
            "Color": 1,
            "Map Pin": 2,
            "3D Transformation": 3,
            "Enlarged Portions": 4,
            "Edge stroke": 5,
            'Highlight Remove': 6,

            "Label Situated": 0,
            "Label Text": 1,
            "Label Icon": 2,
            "Label Color": 3,
            "Label Convenient": 4,
            "Label Aligned": 5,
            "Label Ordered": 6,
            "Label Remove": 7,

            "Color (Luminance)": 0,
            "Color (Hue)": 1,
            "3D Length": 2,
            "Glyph": 3,
            "Link (Line)": 4,
            "Link (Arrow)": 5,
            "Size": 6,
            "Quantity": 7,
            "2D Length": 8,
            "Remove": 9,

        },
    }),

    mounted() {
        console.log(this.value, "created, numerical:", this.isNumerical);
        console.log(this.geoData);

        let worldPopulation = 0;
        if (this.geoData && this.geoData.features && this.infoData) {
            this.geoData.features.forEach(feature => {
                const curPopulation = this.getPopulation(feature)
                worldPopulation += curPopulation;
                this.mostPopulation = this.mostPopulation < curPopulation ? curPopulation : this.mostPopulation;
            });

            console.log(this.mostPopulation);
        }
        this.worldPopulation = worldPopulation;

        const cardEl = this.$refs.selectorCard.$el;
        const legendColEl = this.$refs.legendCol.$el;

        this.$nextTick(() => {
            const height = cardEl.clientHeight;

            const seContainer = document.getElementById(this.value + '-seContainer');
            seContainer.style.maxHeight = (0.99 * height) + "px";

            this.legendWidth = 0.87 * legendColEl.clientWidth;

            this.initMap();
        });
    },

    methods: {
        initMap() {
            // 获得html中的地图（svg）标签
            this.svg = d3.select("." + this.value + "-svg");
            this.legend = d3.select("." + this.value + "-legend");
            this.highLights.push([]);

            //根据窗口大小设置地图的大小
            this.mapWidth = this.svg.node().getBoundingClientRect().width;
            this.mapHeight = 0.8 * this.svg.node().getBoundingClientRect().height;

            this.encodingChannel = () => {
                this.svg.selectAll('path').attr("fill", this.defaultColor);
            };

            this.representation = () => {
                this.svg.selectAll('path')
                    .data(this.geoData.features)
                    .enter()
                    .append('path')
                    .attr('d', this.geoPath)
                    .attr('stroke', '#ffffff');
            };

            // console.log(this.mapWidth, this.mapHeight);
            this.setProjection(1);
            this.drawSvg();
        },

        splitTextToLines(text, maxLineWidth) {
            let words = text.split(' ');
            let lines = [];
            let currentLine = words[0];

            for (let i = 1; i < words.length; i++) {
                if ((currentLine + ' ' + words[i]).length < maxLineWidth) {
                    currentLine += ' ' + words[i];
                } else {
                    lines.push(currentLine);
                    currentLine = words[i];
                }
            }
            lines.push(currentLine); // Add the last line

            return lines;
        },

        //重新绘制svg
        drawSvg() {
            // 移除现有的 SVG
            this.svg.selectAll('*').remove();
            d3.select('#' + this.value + '-enlargedView').selectAll('*').remove();

            this.representation();
            this.encodingChannel();
            this.LabelPosition();

            this.highLights[this.pointer2highlight].forEach(highLight => {
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

        getPopulation(d) {
            // console.log(name, this.infoData[name]);
            return d && d.properties && d.properties.NAME && this.getDataByCountry(d.properties.NAME)
                ? this.getDataByCountry(d.properties.NAME) : -1
        },

        getDataByCountry(cty) {
            return this.infoData[cty] ? Object.values(this.infoData[cty])[0] : undefined;
        },

        getDescriptionByCountry(cty) {
            return this.infoData[cty] && this.infoData[cty]['description'] ? this.infoData[cty]['description'] : undefined;
        },


        showErrorDialog(title, msg) {
            this.errorTitle = title;
            this.errorMessage = msg;
            this.errorDialog = true;
        },

        // 设置 Map Representation
        setRepresentation(type) {
            console.log("Representation:", type)

            if (type === this.myType['Political Map']) {
                this.representationType = type;
                this.representation = () => {
                    this.svg.selectAll('path')
                        .data(this.geoData.features)
                        .enter()
                        .append('path')
                        .attr('d', this.geoPath)
                        .attr('stroke', '#ffffff');
                };
            } else if (type === this.myType['Topographic Map']) {
                this.representationType = type;
            } else if (type === this.myType['Shape-based Map']) {
                this.representationType = type;

                this.representation = () => {
                    // this.svg.selectAll('path')
                    //     .data(this.geoData.features)
                    //     .enter()
                    //     .append('path')
                    //     .attr('d', this.geoPath)
                    //     .attr('stroke', '#ffffff');

                    // 为地图上的每个国家绘制点阵图
                    this.geoData.features.forEach(feature => {
                        // 绘制点
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
                                    points.push({x: x, y: y, properties: feature.properties});
                                }
                            }
                        }

                        this.svg.append('g')
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
                    })
                };
            } else if (type === this.myType['Street Map']) {
                this.representationType = type;
            } else if (type === this.myType['Plain']) {
                this.representationType = type;
                // this.svg.select('.grid-layer').remove();
                // this.svg.select('defs').selectAll('clipPath').remove(); // 假设没有其他clipPath在使用

                this.representation = () => {
                    const addHighLight = (svg) => {
                        const highLight = () => {
                            console.log(svg);
                            d3.select(svg)
                                .classed('highlighted', true) // 使用类来标记高亮
                                .attr('fill', '#000000');
                        };

                        highLight(svg);
                        this.highLights[this.pointer2highlight].push(highLight);
                    };

                    this.svg.selectAll('path')
                        .on('click', function () {
                            addHighLight(this)
                        });
                }


            } else if (type === this.myType['Terrain']) {
                this.representationType = type;

                alert('Attention! Not supporting for ANY color method in encoding channel, label position, or highlight.');

                this.representation = () => {
                    this.svg.append("image")
                    .attr("xlink:href", require("../assets/terrain.svg")) // 设置图片的路径
                    .attr("width", 1000) // 设置图片宽度
                    .attr("height", 750) // 设置图片高度
                    .attr("x", 150) // 设置图片相对于SVG画布的x坐标
                    .attr("y", 0) // 设置图片相对于SVG画布的y坐标
                    .attr('transform', 'scale(1.8, 1.2)');
                };

                
            }

            this.drawSvg();
        },

        // 设置 Map Projection
        setProjection(type) {
            console.log("Map Projection:", type);

            if (type === this.myType['Mercator']) {
                this.projectionType = type;

                this.geoProjection = d3.geoMercator()
                    .fitSize([this.mapWidth, this.mapHeight], this.geoData);
            } else if (type === this.myType['Equirectangular']) {
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
            this.svg.on('click', null);
            // d3.select('#' + this.value + '-enlargedView').selectAll("*").remove(); 
            // 根据类型应用新的高亮方式
            if (type === this.myType['Color']) {
                this.highLightType = type;

                const addHighLight = (svg) => {
                    const highLight = () => {
                        console.log(svg);
                        d3.select(svg)
                            .classed('highlighted', true) // 使用类来标记高亮
                            .attr('fill', '#5959E9');
                    };

                    highLight(svg);
                    this.highLights[this.pointer2highlight].push(highLight);
                };

                this.svg.selectAll('path')
                    .on('click', function () {
                        addHighLight(this)
                    });
            } else if (type === this.myType['Light']) {
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
                    this.highLights[this.pointer2highlight].push(highLight);
                };

                // 绑定一个新的点击事件监听器到SVG本身
                this.svg.on('click', function (event) {
                    addHighLight(event, this)
                });
            } else if (type === this.myType['Map Pin']) {
                this.highLightType = type;

                const addHighLight = (event, svg) => {
                    const [x, y] = d3.pointer(event, svg);

                    const highLight = () => {
                        // 添加一个SVG图标作为光圈效果
                        d3.select(svg).append('image')
                            .classed('highlight-marker', true) // 使用类来标记这是一个高亮标记
                            .attr('xlink:href', require('../assets/locationIcon.svg'))// 设置图像的路径
                            .attr('x', x - 20) // 调整图像位置，使其中心对准点击位置
                            .attr('y', y - 48) // 同上，根据实际大小调整
                            .attr('width', 40) // 设置图像的宽度
                            .attr('height', 48); // 设置图像的高度
                    };

                    highLight();
                    this.highLights[this.pointer2highlight].push(highLight);
                };

                // 绑定一个新的点击事件监听器到SVG本身
                this.svg.on('click', function (event) {
                    addHighLight(event, this);
                });
            } else if (type === this.myType['3D Transformation']) {
                this.highLightType = type;

                const addHighLight = (event, svg) => {
                    // eslint-disable-next-line no-unused-vars
                    const [x, y] = d3.pointer(event, svg);
                    const feature = d3.select(event.target).datum(); // 获取被点击的地图区域的数据
                    const originalColor = d3.select(event.target).attr("fill");

                    // 高亮函数
                    const highLight = () => {
                        // 首先移除之前的高亮效果
                        //this.svg.selectAll('.highlight-3d-effect').remove();

                        // 然后添加一个新的具有3D效果的path
                        this.svg.append('path')
                            .datum(feature) // 使用同一区域的数据
                            .attr('class', 'highlight-3d-effect') // 为了方便之后可能的移除
                            .attr('d', this.geoPath) // 使用geoPath来保持地理形状的一致性
                            .attr('fill', originalColor) // 为了简化，这里使用纯色填充表示阴影
                            .attr('filter', 'url(#drop-shadow)')
                            .attr('stroke-width', 2); // 应用下面定义的SVG滤镜实现阴影效果

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
                    this.highLights[this.pointer2highlight].push(highLight);
                };

                // 绑定点击事件到所有的path上
                this.svg.selectAll('path').on('click', function (event) {
                    addHighLight(event, this);
                });
            } else if (type === this.myType['Enlarged Portions']) {
                this.highLightType = type;

                // 移除之前可能绑定的点击事件以避免重复
                this.svg.on('click', null);

                // 直接在点击事件中实现放大效果的逻辑
                this.svg.on('click', (event) => {
                    // 移除上一次点击留下的圆圈
                    this.svg.selectAll('circle.click-circle').remove();
                    this.svg.selectAll('line.click-circle').remove();

                    const [x, y] = d3.pointer(event, this.svg.node());

                    // 在点击位置绘制一个圆圈作为反馈
                    this.svg.append('circle')
                        .classed('click-circle', true) // 添加一个类以便后续可以选择并移除
                        .attr('cx', x)
                        .attr('cy', y)
                        .attr('r', 30) // 圆的半径
                        .style('fill', 'none')
                        .style('stroke', '#5959E9')
                        .style('stroke-width', 3);

                    // 清除#enlargedView中的内容
                    const enlargedView = d3.select('#' + this.value + '-enlargedView');
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
                        .style('transform', ` scale(2)`);

                    // draw traction line
                    const x1 = this.mapWidth - 94, y1 = 147, r1 = 100, r = 30; // approximate centre of enlarged circle
                    const d = Math.sqrt((x1 - x) * (x1 - x) + (y1 - y) * (y1 - y));
                    const xa = x + r * Math.cos(Math.atan((y1 - y) / (x1 - x)) + Math.acos((r - r1) / d));
                    const ya = y + r * Math.sin(Math.atan((y1 - y) / (x1 - x)) + Math.acos((r - r1) / d));
                    const xb = x1 + r1 * Math.cos(Math.atan((y1 - y) / (x1 - x)) + Math.acos((r - r1) / d));
                    const yb = y1 + r1 * Math.sin(Math.atan((y1 - y) / (x1 - x)) + Math.acos((r - r1) / d));
                    const xc = x + r * Math.cos(Math.atan((y1 - y) / (x1 - x)) - Math.acos((r - r1) / d));
                    const yc = y + r * Math.sin(Math.atan((y1 - y) / (x1 - x)) - Math.acos((r - r1) / d));
                    const xd = x1 + r1 * Math.cos(Math.atan((y1 - y) / (x1 - x)) - Math.acos((r - r1) / d));
                    const yd = y1 + r1 * Math.sin(Math.atan((y1 - y) / (x1 - x)) - Math.acos((r - r1) / d));
                    this.svg.append('line')
                        .classed('click-circle', true)
                        .attr('x1', xa)
                        .attr('y1', ya)
                        .attr('x2', xb)
                        .attr('y2', yb)
                        .attr('stroke', 'grey')
                        .attr('stroke-width', 1);
                    this.svg.append('line')
                        .classed('click-circle', true)
                        .attr('x1', xc)
                        .attr('y1', yc)
                        .attr('x2', xd)
                        .attr('y2', yd)
                        .attr('stroke', 'grey')
                        .attr('stroke-width', 1);
                });
            } else if (type === this.myType['Edge Stroke']) {
                this.highLightType = type;

                const addHighLight = (event) => {
                    const feature = d3.select(event.target).datum(); // 获取被点击的地图区域的数据

                    // 高亮函数
                    const highLight = () => {
                        this.svg.append('path')
                            .datum(feature) // 使用同一区域的数据
                            .attr('class', 'highlight-edge-stroke') // 为了方便之后可能的移除
                            .attr('d', this.geoPath) // 使用geoPath来保持地理形状的一致性
                            .attr('stroke-width', 2)
                            .attr('stroke', '#5959E9')
                            .style('fill', 'none');
                    };

                    highLight();
                    this.highLights[this.pointer2highlight].push(highLight);
                };

                // 绑定点击事件到所有的path上
                this.svg.selectAll('path').on('click', function (event) {
                    addHighLight(event, this);
                });
            } else if (type === this.myType['Highlight Remove']) {
                this.highLightType = type;
                this.highLights.push([]);
                this.pointer2highlight++;
                this.drawSvg();
            }


        },

        setLabelPosition(type) {
            console.log("Label Position:", type);
            // 移除之前添加的所有标签
            this.svg.selectAll(".country-label, .annotation-box, .annotation-text, .olympic-label, .country-flag, .annotation-line").remove();
            this.svg.selectAll(".country-color")
                .style('fill', null) // 或设置为你的默认颜色
                .classed("country-color", false); // 移除类，以避免对后续操作的影响
            // 定义注解框的宽度、高度和间距
            const boxWidth = 200; // 固定宽度
            const boxHeight = 60; // 固定高度
            const boxSpacing = 20; // 注解框之间的间距
            if (type === this.myType['Label Situated']) {
                this.labelPositionType = type;

                this.LabelPosition = () => {
                    this.geoData.features.forEach(feature => {
                        const center = this.geoPath.centroid(feature);
                        const annotation = feature.properties.annotation;

                        if (annotation && annotation != -1) {
                            let textLines = [
                                `Country: ${feature.properties.NAME}`,
                                `City: ${annotation.city}`
                            ];

                            // 根据条件动态添加Summer和Winter的行
                            if (annotation.summer_olympics && annotation.summer_olympics.length > 0) {
                                textLines.push(`Summer: ${annotation.summer_olympics}`);
                            }
                            if (annotation.winter_olympics && annotation.winter_olympics.length > 0) {
                                textLines.push(`Winter: ${annotation.winter_olympics}`);
                            }
                            const maxLineWidth = 30;

                            // 用于跟踪当前垂直位置的变量
                            let currentYOffset = 0;

                            // 应用拆分函数并添加文本
                            textLines.forEach((line) => {
                                let subLines = this.splitTextToLines(line, maxLineWidth); // 使用拆分函数
                                subLines.forEach((subLine) => {
                                    this.svg.append('text')
                                        .attr('class', 'olympic-label')
                                        .attr('x', center[0])
                                        .attr('y', center[1] + currentYOffset) // 使用currentYOffset确定垂直位置
                                        .attr('text-anchor', 'middle')
                                        .attr('fill', 'black')
                                        .style('font-size', '8px')
                                        .text(subLine);

                                    // 每添加一行，更新currentYOffset以便下一行下移
                                    currentYOffset += 10; // 假设每行文本的高度加间距为15px
                                });

                                // 注意：这里不再需要调整index
                            });
                        }
                    });
                }


            } else if (type === this.myType['Label Text']) {
                this.labelPositionType = type;

                this.LabelPosition = () => {
                    // 仅为olympics_data.json中存在的国家显示国家名字
                    this.geoData.features.forEach(feature => {
                        if (feature.properties.annotation != -1) {
                            const center = this.geoPath.centroid(feature);
                            this.svg.append('text')
                                .attr('class', 'country-label')
                                .attr('x', center[0])
                                .attr('y', center[1])
                                .attr('text-anchor', 'middle')
                                .attr('fill', 'black')
                                .style('font-size', '15px')
                                .text(feature.properties.NAME);
                        }
                    });

                    // 过滤掉不需要展示注解的数据
                    const annotatedFeatures = this.geoData.features.filter(feature => feature.properties.annotation && feature.properties.annotation != -1);

                    // 用于注解的特征进行循环，而不是所有特征
                    annotatedFeatures.forEach((feature, index) => {
                        const annotation = feature.properties.annotation;


                        // // 动态计算x坐标，考虑间距，以保证注解框在水平方向上均匀对齐
                        // const x = col * (boxWidth + boxSpacing);

                        // 计算每个注解的起始x坐标
                        const totalAnnotationsWidth = annotatedFeatures.length * (boxWidth + boxSpacing) - boxSpacing; // 总宽度减去最后一个间距
                        const startX = (this.mapWidth - totalAnnotationsWidth) / 2; // 为了居中对齐
                        // // 调整y坐标，为每个注解框下方留出一定的间距
                        // const y = this.mapHeight + row * (boxHeight + 20 + boxSpacing); // 调整了间距的计算
                        const annotationX = startX + index * (boxWidth + boxSpacing); 
                        const annotationY = this.mapHeight + 50; // 地图下方50px


                        // 绘制注解框
                        // this.svg.append('rect')
                        //     .attr('class', 'annotation-box')
                        //     .attr('x', annotationX)
                        //     .attr('y', annotationY)
                        //     .attr('width', boxWidth)
                        //     .attr('height', boxHeight)
                        //     .attr('fill', this.defaultColor)
                        //     .attr('stroke', 'none');

                        // 在注解框内添加文本
                        let textLines = [
                            `Country: ${feature.properties.NAME}`,
                            `City: ${annotation.city}`
                        ];

                        // 根据条件动态添加Summer和Winter的行
                        if (annotation.summer_olympics && annotation.summer_olympics.length > 0) {
                            textLines.push(`Summer: ${annotation.summer_olympics}`);
                        }
                        if (annotation.winter_olympics && annotation.winter_olympics.length > 0) {
                            textLines.push(`Winter: ${annotation.winter_olympics}`);
                        }

                        const maxWidth = boxWidth-5; // 设置最大宽度阈值
                        let ty = annotationY;

                        textLines.forEach((line, lineIndex) => {
                            let words = line.split(' ');
                            let currentLine = words[0];

                            for (let i = 1; i < words.length; i++) {
                                let word = words[i];
                                let testLine = currentLine + ' ' + word;
                                let testWidth = this.getTextWidth(testLine, '10px'); // 获取当前行的文本宽度

                                if (testWidth > maxWidth) {
                                    this.svg.append('text')
                                        .attr('class', 'annotation-text')
                                        .attr('x', annotationX + 5) // 略微缩进
                                        .attr('y', ty + 15 + (lineIndex * 12)) // 根据行数调整位置
                                        .attr('fill', 'black')
                                        .style('font-size', '10px')
                                        .text(currentLine); // 添加当前行的文本

                                    currentLine = word;
                                    ty += 12; // 调整Y坐标到下一行
                                } else {
                                    currentLine += ' ' + word;
                                }
                            }
                        });

                        this.svg.append('rect')
                            .attr('class', 'annotation-box')
                            .attr('x', annotationX)
                            .attr('y', annotationY)
                            .attr('width', boxWidth)
                            .attr('height', boxHeight+ty-annotationY)
                            .attr('fill', this.defaultColor)
                            .attr('stroke', 'none');

                        ty = annotationY;
                        textLines.forEach((line, lineIndex) => {
                            let words = line.split(' ');
                            let currentLine = words[0];

                            for (let i = 1; i < words.length; i++) {
                                let word = words[i];
                                let testLine = currentLine + ' ' + word;
                                let testWidth = this.getTextWidth(testLine, '10px'); // 获取当前行的文本宽度

                                if (testWidth > maxWidth) {
                                    this.svg.append('text')
                                        .attr('class', 'annotation-text')
                                        .attr('x', annotationX + 5) // 略微缩进
                                        .attr('y', ty + 15 + (lineIndex * 12)) // 根据行数调整位置
                                        .attr('fill', 'black')
                                        .style('font-size', '10px')
                                        .text(currentLine); // 添加当前行的文本

                                    currentLine = word;
                                    ty += 12; // 调整Y坐标到下一行
                                } else {
                                    currentLine += ' ' + word;
                                }
                            }
                            this.svg.append('text')
                                .attr('class', 'annotation-text')
                                .attr('x', annotationX + 5) // 略微缩进
                                .attr('y', ty + 15 + (lineIndex * 12)) // 根据行数调整位置
                                .attr('fill', 'black')
                                .style('font-size', '10px')
                                .text(currentLine);
                        });
                    });
                }

            } else if (type === this.myType['Label Icon']) {
                this.labelPositionType = type;

                this.LabelPosition = () => {
                    // 过滤掉不需要展示注解的数据
                    const annotatedFeatures = this.geoData.features.filter(feature => feature.properties.annotation && feature.properties.annotation != -1);


                    // 用于注解的特征进行循环
                    annotatedFeatures.forEach((feature, index) => {
                        const annotation = feature.properties.annotation;
                        // 计算每个注解的起始x坐标
                        const totalAnnotationsWidth = annotatedFeatures.length * (boxWidth + boxSpacing) - boxSpacing; // 总宽度减去最后一个间距
                        const startX = (this.mapWidth - totalAnnotationsWidth) / 2; // 为了居中对齐
                        // // 调整y坐标，为每个注解框下方留出一定的间距
                        // const y = this.mapHeight + row * (boxHeight + 20 + boxSpacing); // 调整了间距的计算
                        const annotationX = startX + index * (boxWidth + boxSpacing);
                        const annotationY = this.mapHeight + 50; // 地图下方50px
                        if (annotation && annotation.flag_base64) {
                            const center = this.geoPath.centroid(feature);
                            // 在地图的国家中心点上添加国旗图像
                            this.svg.append('image')
                                .attr('xlink:href', annotation.flag_base64)
                                .attr('x', center[0] - 15) // 调整这个值以适合国旗图像的大小和位置
                                .attr('y', center[1] - 10)
                                .attr('width', 30) // 根据需要调整国旗的尺寸
                                .attr('height', 20)
                                .attr('class', 'country-flag');


                            // 先绘制注解框作为背景
                            this.svg.append('rect')
                                .attr('class', 'annotation-box')
                                .attr('x', annotationX)
                                .attr('y', annotationY-boxHeight)
                                .attr('width', boxWidth)
                                .attr('height', boxHeight)
                                .attr('fill', 'url(#flagPattern' + index + ')') // 使用图案填充
                                .attr('stroke', 'none');

                            let textLines = [
                                `Country: ${feature.properties.NAME}`,
                                `City: ${annotation.city}`
                            ];

                            // 根据条件动态添加Summer和Winter的行
                            if (annotation.summer_olympics && annotation.summer_olympics.length > 0) {
                                textLines.push(`Summer: ${annotation.summer_olympics}`);
                            }
                            if (annotation.winter_olympics && annotation.winter_olympics.length > 0) {
                                textLines.push(`Winter: ${annotation.winter_olympics}`);
                            }

                            const maxWidth = boxWidth-5; // 设置最大宽度阈值
                            let ty = annotationY;

                            textLines.forEach((line, lineIndex) => {
                                let words = line.split(' ');
                                let currentLine = words[0];

                                for (let i = 1; i < words.length; i++) {
                                    let word = words[i];
                                    let testLine = currentLine + ' ' + word;
                                    let testWidth = this.getTextWidth(testLine, '10px'); // 获取当前行的文本宽度

                                    if (testWidth > maxWidth) {
                                        this.svg.append('text')
                                            .attr('class', 'annotation-text')
                                            .attr('x', annotationX + 5) // 略微缩进
                                            .attr('y', ty + 15 + (lineIndex * 12)) // 根据行数调整位置
                                            .attr('fill', 'black')
                                            .style('font-size', '10px')
                                            .text(currentLine); // 添加当前行的文本

                                        currentLine = word;
                                        ty += 12; // 调整Y坐标到下一行
                                    } else {
                                        currentLine += ' ' + word;
                                    }
                                }
                            });

                            this.svg.append('rect')
                                .attr('class', 'annotation-box')
                                .attr('x', annotationX)
                                .attr('y', annotationY)
                                .attr('width', boxWidth)
                                .attr('height', boxHeight+ty-annotationY)
                                .attr('fill', this.defaultColor)
                                .attr('stroke', 'none');

                            ty = annotationY;
                            textLines.forEach((line, lineIndex) => {
                                let words = line.split(' ');
                                let currentLine = words[0];

                                for (let i = 1; i < words.length; i++) {
                                    let word = words[i];
                                    let testLine = currentLine + ' ' + word;
                                    let testWidth = this.getTextWidth(testLine, '10px'); // 获取当前行的文本宽度

                                    if (testWidth > maxWidth) {
                                        this.svg.append('text')
                                            .attr('class', 'annotation-text')
                                            .attr('x', annotationX + 5) // 略微缩进
                                            .attr('y', ty + 15 + (lineIndex * 12)) // 根据行数调整位置
                                            .attr('fill', 'black')
                                            .style('font-size', '10px')
                                            .text(currentLine); // 添加当前行的文本

                                        currentLine = word;
                                        ty += 12; // 调整Y坐标到下一行
                                    } else {
                                        currentLine += ' ' + word;
                                    }
                                }
                                this.svg.append('text')
                                    .attr('class', 'annotation-text')
                                    .attr('x', annotationX + 5) // 略微缩进
                                    .attr('y', ty + 15 + (lineIndex * 12)) // 根据行数调整位置
                                    .attr('fill', 'black')
                                    .style('font-size', '10px')
                                    .text(currentLine);
                            });

                            // 创建用于国旗背景的图案
                            this.svg.append('pattern')
                                .attr('id', 'flagPattern' + index)
                                .attr('patternUnits', 'objectBoundingBox')
                                .attr('width', '100%')
                                .attr('height', '100%')
                                .append('image')
                                .attr('xlink:href', annotation.flag_base64)
                                .attr('width', boxWidth)
                                .attr('height', boxHeight)
                                .attr('preserveAspectRatio', 'xMidYMid slice');
                        }
                    });
                }

            } else if (type === this.myType['Label Color']) {
                this.labelPositionType = type;

                this.LabelPosition = () => {
                    // 颜色数组
                    const countryColors = ["#8ECFC9", "#FFBE7A", "#FA7F6F", "#82B0D2", "#BEB8DC", "#F6CAE5", "#F1D77E", "#2878b5", "#779043"];
                    const getCountryColor = (index) => countryColors[index % countryColors.length];

                    // 过滤出需要注解的国家特征
                    const annotatedFeatures = this.geoData.features.filter(feature => feature.properties.annotation && feature.properties.annotation != -1);

                    // 为有注解的国家设置颜色
                    annotatedFeatures.forEach((feature, index) => {
                        // 计算每个注解的起始x坐标
                        const totalAnnotationsWidth = annotatedFeatures.length * (boxWidth + boxSpacing) - boxSpacing; // 总宽度减去最后一个间距
                        const startX = (this.mapWidth - totalAnnotationsWidth) / 2; // 为了居中对齐
                        // // 调整y坐标，为每个注解框下方留出一定的间距
                        // const y = this.mapHeight + row * (boxHeight + 20 + boxSpacing); // 调整了间距的计算
                        const annotationX = startX + index * (boxWidth + boxSpacing);
                        const annotationY = this.mapHeight + 50; // 地图下方50px
                        const fillColor = getCountryColor(index); // 获取颜色

                        // 设置国家颜色
                        this.svg.selectAll('path')
                            .filter(d => d === feature)
                            .style('fill', fillColor)
                            .classed("country-color", true);

                        // 创建注解框
                        // this.svg.append('rect')
                        //     .attr('class', 'annotation-box')
                        //     .attr('x', annotationX)
                        //     .attr('y', annotationY)
                        //     .attr('width', boxWidth)
                        //     .attr('height', boxHeight)
                        //     .attr('fill', fillColor) // 确保注解框颜色与国家颜色相同
                        //     .attr('stroke', 'none');

                        // 添加注解文本
                        const annotation = feature.properties.annotation;
                        let textLines = [
                            `Country: ${feature.properties.NAME}`,
                            `City: ${annotation.city}`
                        ];

                        // 根据条件动态添加Summer和Winter的行
                        if (annotation.summer_olympics && annotation.summer_olympics.length > 0) {
                            textLines.push(`Summer: ${annotation.summer_olympics}`);
                        }
                        if (annotation.winter_olympics && annotation.winter_olympics.length > 0) {
                            textLines.push(`Winter: ${annotation.winter_olympics}`);
                        }

                        const maxWidth = boxWidth-5; // 设置最大宽度阈值
                        let ty = annotationY;

                        textLines.forEach((line, lineIndex) => {
                            let words = line.split(' ');
                            let currentLine = words[0];

                            for (let i = 1; i < words.length; i++) {
                                let word = words[i];
                                let testLine = currentLine + ' ' + word;
                                let testWidth = this.getTextWidth(testLine, '10px'); // 获取当前行的文本宽度

                                if (testWidth > maxWidth) {
                                    this.svg.append('text')
                                        .attr('class', 'annotation-text')
                                        .attr('x', annotationX + 5) // 略微缩进
                                        .attr('y', ty + 15 + (lineIndex * 12)) // 根据行数调整位置
                                        .attr('fill', 'black')
                                        .style('font-size', '10px')
                                        .text(currentLine); // 添加当前行的文本

                                    currentLine = word;
                                    ty += 12; // 调整Y坐标到下一行
                                } else {
                                    currentLine += ' ' + word;
                                }
                            }
                        });

                        this.svg.append('rect')
                            .attr('class', 'annotation-box')
                            .attr('x', annotationX)
                            .attr('y', annotationY)
                            .attr('width', boxWidth)
                            .attr('height', boxHeight+ty-annotationY)
                            .attr('fill', fillColor)
                            .attr('stroke', 'none');

                        ty = annotationY;
                        textLines.forEach((line, lineIndex) => {
                            let words = line.split(' ');
                            let currentLine = words[0];

                            for (let i = 1; i < words.length; i++) {
                                let word = words[i];
                                let testLine = currentLine + ' ' + word;
                                let testWidth = this.getTextWidth(testLine, '10px'); // 获取当前行的文本宽度

                                if (testWidth > maxWidth) {
                                    this.svg.append('text')
                                        .attr('class', 'annotation-text')
                                        .attr('x', annotationX + 5) // 略微缩进
                                        .attr('y', ty + 15 + (lineIndex * 12)) // 根据行数调整位置
                                        .attr('fill', 'black')
                                        .style('font-size', '10px')
                                        .text(currentLine); // 添加当前行的文本

                                    currentLine = word;
                                    ty += 12; // 调整Y坐标到下一行
                                } else {
                                    currentLine += ' ' + word;
                                }
                            }
                            this.svg.append('text')
                                .attr('class', 'annotation-text')
                                .attr('x', annotationX + 5) // 略微缩进
                                .attr('y', ty + 15 + (lineIndex * 12)) // 根据行数调整位置
                                .attr('fill', 'black')
                                .style('font-size', '10px')
                                .text(currentLine);
                        });
                    });
                }


            } else if (type === this.myType['Label Convenient']) {
                this.labelPositionType = type;
                this.LabelPosition = () => {
                    const annotatedFeatures = this.geoData.features.filter(feature => feature.properties.annotation && feature.properties.annotation != -1);
                    const totalAnnotations = annotatedFeatures.length;

                    // 假设每边分配的注解数量大致相等
                    const annotationsPerSide = Math.ceil(totalAnnotations / 3);
                    // eslint-disable-next-line
                    let leftAnnotationsCount = 0, bottomAnnotationsCount = 0, rightAnnotationsCount = 0;

                    annotatedFeatures.forEach((feature) => {
                        const countryCenter = this.geoPath.centroid(feature);
                        const annotation = feature.properties.annotation;

                        // 特定国家（如"Austria"）的连线长度
                        const lineLength = feature.properties.NAME === "Austria" ? 400 : 300;

                        // 计算到三边的距离
                        const distanceToLeft = countryCenter[0];
                        const distanceToBottom = this.mapHeight - countryCenter[1];
                        const distanceToRight = this.mapWidth - countryCenter[0];

                        // 确定注解应放置在哪个边缘
                        let edge = 'left'; // 默认左边
                        let minDistance = distanceToLeft;

                        if (distanceToBottom < minDistance && bottomAnnotationsCount < annotationsPerSide) {
                            minDistance = distanceToBottom;
                            edge = 'bottom';
                        }
                        if (distanceToRight < minDistance && rightAnnotationsCount < annotationsPerSide) {
                            edge = 'right';
                        }

                        // 更新对应边缘的注解计数
                        if (edge === 'left') leftAnnotationsCount++;
                        else if (edge === 'bottom') bottomAnnotationsCount++;
                        else rightAnnotationsCount++;

                        // 计算线的终点位置
                        let lineEndX = countryCenter[0], lineEndY = countryCenter[1];
                        let textOffsetX = countryCenter[0], textOffsetY = countryCenter[1];

                        switch (edge) {
                            case 'left':
                                lineEndX -= lineLength;
                                textOffsetX = lineEndX - boxWidth - 5;
                                textOffsetY = countryCenter[1] - boxHeight / 2;
                                break;
                            case 'bottom':
                                lineEndY += lineLength;
                                textOffsetX = countryCenter[0] - boxWidth / 2;
                                textOffsetY = lineEndY + 5;
                                break;
                            case 'right':
                                lineEndX += lineLength;
                                textOffsetX = lineEndX + 5;
                                textOffsetY = countryCenter[1] - boxHeight / 2;
                                break;
                        }
                        // 绘制注解连线
                        this.svg.append('line')
                            .attr('x1', countryCenter[0])
                            .attr('y1', countryCenter[1])
                            .attr('x2', lineEndX)
                            .attr('y2', lineEndY)
                            .attr('stroke', 'black')
                            .attr('stroke-width', 1)
                            .attr('class', 'annotation-line');

                        // 绘制文本框背景
                        this.svg.append('rect')
                            .attr('x', textOffsetX)
                            .attr('y', textOffsetY)
                            .attr('width', boxWidth)
                            .attr('height', boxHeight)
                            .attr('fill', 'white')
                            .attr('stroke', 'black')
                            .attr('class', 'annotation-box');

                        let textLines = [
                            `Country: ${feature.properties.NAME}`,
                            `City: ${annotation.city}`
                        ];

                        // 根据条件动态添加Summer和Winter的行
                        if (annotation.summer_olympics && annotation.summer_olympics.length > 0) {
                            textLines.push(`Summer: ${annotation.summer_olympics}`);
                        }
                        if (annotation.winter_olympics && annotation.winter_olympics.length > 0) {
                            textLines.push(`Winter: ${annotation.winter_olympics}`);
                        }

                        // 添加多行注解文本
                        textLines.forEach((line, i) => {
                            this.svg.append('text')
                                .attr('x', textOffsetX + 5)
                                .attr('y', textOffsetY + 13 + i * 13)
                                .attr('fill', 'black')
                                .style('font-size', '10px')
                                .text(line)
                                .attr('class', 'annotation-text');
                        });
                    });
                }


            } else if (type === this.myType['Label Aligned']) {
                this.labelPositionType = type;

                this.LabelPosition = () => {
                    const sortedFeatures = this.geoData.features
                        .filter(feature => feature.properties.annotation && feature.properties.annotation != -1)
                        .sort((a, b) => {
                            const centerA = this.geoPath.centroid(a);
                            const centerB = this.geoPath.centroid(b);
                            return centerA[0] - centerB[0];
                        });

                    // 计算每个注解的起始x坐标
                    const totalAnnotationsWidth = sortedFeatures.length * (boxWidth + boxSpacing) - boxSpacing; // 总宽度减去最后一个间距
                    const startX = (this.mapWidth - totalAnnotationsWidth) / 2; // 为了居中对齐

                    sortedFeatures.forEach((feature, index) => {
                        const annotation = feature.properties.annotation;
                        const countryCenter = this.geoPath.centroid(feature);
                        const annotationX = startX + index * (boxWidth + boxSpacing);
                        const annotationY = this.mapHeight + 50; // 地图下方50px

                        // 绘制注解框
                        this.svg.append('rect')
                            .attr('class', 'annotation-box')
                            .attr('x', annotationX)
                            .attr('y', annotationY)
                            .attr('width', boxWidth)
                            .attr('height', boxHeight)
                            .attr('fill', 'none')
                            .attr('stroke', 'black');

                        // 准备注解文本
                        let textLines = [
                            `Country: ${feature.properties.NAME}`,
                            `City: ${annotation.city}`
                        ];

                        // 根据条件动态添加Summer和Winter的行
                        if (annotation.summer_olympics && annotation.summer_olympics.length > 0) {
                            textLines.push(`Summer: ${annotation.summer_olympics}`);
                        }
                        if (annotation.winter_olympics && annotation.winter_olympics.length > 0) {
                            textLines.push(`Winter: ${annotation.winter_olympics}`);
                        }

                        // 在注解框内添加文本
                        textLines.forEach((line, lineIndex) => {
                            this.svg.append('text')
                                .attr('class', 'annotation-text')
                                .attr('x', annotationX + 5) // 略微缩进
                                .attr('y', annotationY + 15 + (lineIndex * 12)) // 调整文本的垂直位置
                                .attr('fill', 'black')
                                .style('font-size', '10px')
                                .text(line);
                        });

                        // 绘制注解连线
                        this.svg.append('path')
                            .attr('d', `M${countryCenter[0]} ${countryCenter[1]} L${annotationX + boxWidth / 2} ${countryCenter[1]} L${annotationX + boxWidth / 2} ${annotationY}`)
                            .attr('stroke', 'black')
                            .attr('fill', 'none')
                            .attr('class', 'annotation-line');
                    });
                }
                // 过滤并排序需要注解的国家特征，基于它们的中心x坐标

            } else if (type === this.myType['Label Ordered']) {
                this.labelPositionType = type;

                this.LabelPosition = () => {
                    const annotatedFeatures = this.geoData.features.filter(feature => feature.properties.annotation && feature.properties.annotation != -1);
                    const circleCenterX = 500; // 圆心的x坐标
                    const circleCenterY = this.mapHeight - 100; // 圆心的y坐标
                    const radius = Math.min(this.mapWidth, this.mapHeight) / 3; // 半径
                    const angleIncrement = (2 * Math.PI) / annotatedFeatures.length; // 每个注解之间的角度增量
                    let delta = -6;
                    const gamma = 2;

                    annotatedFeatures.forEach((feature, index) => {
                        delta += gamma;
                        const angle = angleIncrement * index;
                        const annotationX = circleCenterX + radius * Math.cos(angle);
                        const annotationY = circleCenterY + radius * Math.sin(angle);
                        const countryCenter = this.geoPath.centroid(feature);
                        // 更改连线到注解的最近的边缘中心点
                        const lineEndX = annotationX+delta;
                        const lineEndY = (countryCenter[1] < annotationY ? annotationY - boxHeight / 2 : annotationY + boxHeight / 2) + delta;

                        this.svg.append('path')
                            .attr('d', `M${countryCenter[0]+delta} ${countryCenter[1]+delta} L${lineEndX} ${countryCenter[1]+delta} L${lineEndX} ${lineEndY}`)
                            .attr('stroke', 'gray')
                            .attr('fill', 'none')
                            .attr('class', 'annotation-line');

                        // 准备注解文本
                        let textLines = [
                            `Country: ${feature.properties.NAME}`,
                            `City: ${feature.properties.annotation.city}`
                        ];

                        if (feature.properties.annotation.summer_olympics && feature.properties.annotation.summer_olympics.length > 0) {
                            textLines.push(`Summer: ${feature.properties.annotation.summer_olympics}`);
                        }
                        if (feature.properties.annotation.winter_olympics && feature.properties.annotation.winter_olympics.length > 0) {
                            textLines.push(`Winter: ${feature.properties.annotation.winter_olympics}`);
                        }

                        // 绘制注解框
                        this.svg.append('rect')
                            .attr('class', 'annotation-box')
                            .attr('x', annotationX - boxWidth / 2 + delta) // 中心对齐调整
                            .attr('y', annotationY - boxHeight / 2 + delta) // 中心对齐调整
                            .attr('width', boxWidth)
                            .attr('height', boxHeight)
                            .attr('fill', 'none')
                            .attr('stroke', 'black');

                        // 在注解框内添加多行文本
                        textLines.forEach((line, lineIndex) => {
                            this.svg.append('text')
                                .attr('class', 'annotation-text')
                                .attr('x', annotationX + delta)
                                .attr('y', annotationY - boxHeight / 2 + 10 + lineIndex * 15 + delta) // 垂直位置调整
                                .attr('text-anchor', 'middle')
                                .attr('fill', 'black')
                                .style('font-size', '10px')
                                .text(line);
                        });


                    });
                }

            } else if (type === this.myType['Label Remove']) {
                this.labelPositionType = type;
                this.LabelPosition = () => {
                    console.log("All Label Removed!");
                }
            }
            this.drawSvg();

        },

        setEncodingChannel(type) {
            console.log("Encoding Channel:", type);
            //d3.select("." + this.value + "-legend").selectAll("*").remove();
            if (this.isNumerical) {
                //Encoding Color (Luminance)'
                if (type === this.myType['Color (Luminance)']) {
                    d3.select("." + this.value + "-legend").selectAll("*").remove();
                    this.preColortype = type;
                    this.encodingChannelType = type;
                    const colorFunction = (scale) => {
                        const transformFunction = (input) => Math.pow(input, 0.25);
                        // const transformFunction = (input) => input

                        const colorScale = d3.scaleSequential(d3.interpolateRgb(d3.rgb(220, 120, 130), d3.rgb(255, 255, 255)))
                            .domain([transformFunction(this.mostPopulation), 0]);
                        return scale == -1 ? this.defaultColor : colorScale(transformFunction(scale));
                    }
                    this.colorFunctionL = colorFunction;
                    // 重写encodingChannel函数
                    if (this.ifDoubleEncoding == false) {
                        this.encodingChannel = () => {
                            // 修改颜色映射的方法
                            this.svg.selectAll('path')
                                .attr('fill', d => colorFunction(this.getPopulation(d)));

                            this.svg.selectAll('circle')
                                .attr('fill', d => colorFunction(this.getPopulation(d)));
                            this.highLights[this.pointer2highlight].forEach(highLight => {
                                highLight();
                            });
                        }
                        this.drawColorLuminanceLegend();
                    } else {
                        this.preEncoding = type;
                        this.svg.selectAll('path')
                            .attr('fill', `${this.defaultColor}`);
                        this.svg.selectAll('circle')
                            .attr('fill', `${this.defaultColor}`);
                    }
                }

                //Encoding Color (Hue)'
                else if (type === this.myType['Color (Hue)']) {
                    d3.select("." + this.value + "-legend").selectAll("*").remove();
                    this.preColortype = type;
                    this.encodingChannelType = type;
                    const colorFunction = (population) => {
                        if (population < 0) {
                            return this.defaultColor;
                        } else if (population >= 0 && population < 5000000) {
                            return 'rgb(142, 207, 201)'; // 人口数量小于5000000
                        } else if (population >= 5000000 && population < 10000000) {
                            return 'rgb(255, 190, 122)'; // 人口数量在5000000-10000000之间
                        } else if (population >= 10000000 && population < 50000000) {
                            return 'rgb(250, 127, 111)'; // 人口数量在10000000-50000000之间
                        } else if (population >= 50000000 && population < 100000000) {
                            return 'rgb(130, 176, 210)'; // 人口数量在50000000-100000000之间
                        } else {
                            return 'rgb(190, 184, 220)'; // 人口数量大于100000000
                        }
                    };
                    // 重写encodingChannel函数
                    if (this.ifDoubleEncoding == false) {
                        this.encodingChannel = () => {
                            // 修改颜色映射的方法
                            this.svg.selectAll('path')
                                .attr('fill', d => colorFunction(this.getPopulation(d)));

                            this.svg.selectAll('circle')
                                .attr('fill', d => colorFunction(this.getPopulation(d)));
                            this.highLights[this.pointer2highlight].forEach(highLight => {
                                highLight();
                            });
                        };
                        this.drawColorHueLegend();
                    } else {
                        this.preEncoding = type;
                        this.colorFunctionL = colorFunction;
                        this.svg.selectAll('path')
                            .attr('fill', this.defaultColor);
                        this.svg.selectAll('circle')
                            .attr('fill', this.defaultColor);
                    }
                }
                //Encoding 3D Length
                else if (type === this.myType['3D Length']) {
                    d3.select("." + this.value + "-legend").selectAll("*").remove();
                    this.encodingChannelType = type;

                    this.encodingChannel = () => {
                        this.svg.selectAll('path').attr("fill", this.defaultColor);

                        // 在地图上绘制模拟的3D长方体
                        const baseHeight = 3; // 长方体基础高度，所有长方体至少有这个高度
                        const populationPerHeight = 800000; // 每增加这么多人口，长方体的高度增加一单位
                        const cuboidWidth = 20; // 长方体的宽度
                        const cuboidLength = 30; // 长方体的长度（在SVG中模拟的“深度”）
                        const sideOpacity = 0.5; // 侧面的不透明度

                        this.geoData.features.forEach(feature => {
                            const center = this.geoPath.centroid(feature);
                            const population = this.getPopulation(feature);
                            if (population >= 1000000) { // 人口大于等于1000000时绘制长方体
                                const height = baseHeight + (population / populationPerHeight); // 长方体的总高度

                                if (this.ifDoubleEncoding == false) {
                                    // 绘制长方体的“前面”
                                    this.svg.append('rect')
                                        .attr('x', center[0] - cuboidWidth / 2)
                                        .attr('y', center[1] - height)
                                        .attr('width', cuboidWidth)
                                        .attr('height', height)
                                        .attr('fill', 'rgba(230, 158, 165, 0.8)'); // 修改前面的颜色

                                    // 绘制长方体的“顶面”
                                    this.svg.append('polygon')
                                        .attr('points', `${center[0] - cuboidWidth / 2},${center[1] - height} ${center[0] + cuboidWidth / 2},${center[1] - height} ${center[0] + cuboidWidth / 2 - cuboidLength / 4},${center[1] - height - cuboidLength / 4} ${center[0] - cuboidWidth / 2 - cuboidLength / 4},${center[1] - height - cuboidLength / 4}`)
                                        .attr('fill', 'rgba(230, 158, 165, 0.6)');

                                    // 绘制长方体的“左侧面”
                                    this.svg.append('polygon')
                                        .attr('points', `${center[0] - cuboidWidth / 2},${center[1]} ${center[0] - cuboidWidth / 2},${center[1] - height} ${center[0] - cuboidWidth / 2 - cuboidLength / 4},${center[1] - height - cuboidLength / 4} ${center[0] - cuboidWidth / 2 - cuboidLength / 4},${center[1] - cuboidLength / 4}`)
                                        .attr('fill', `rgba(200, 60, 60, ${sideOpacity})`); // 修改左侧面的颜色
                                } else {
                                    // 绘制长方体的“前面”                     
                                    this.svg.append('rect')
                                        .attr('x', center[0] - cuboidWidth / 2)
                                        .attr('y', center[1] - height)
                                        .attr('width', cuboidWidth)
                                        .attr('height', height)
                                        .attr('fill', this.colorFunctionL(population))
                                        .attr('opacity', '0.8'); // 修改前面的颜色

                                    // 绘制长方体的“顶面”
                                    this.svg.append('polygon')
                                        .attr('points', `${center[0] - cuboidWidth / 2},${center[1] - height} ${center[0] + cuboidWidth / 2},${center[1] - height} ${center[0] + cuboidWidth / 2 - cuboidLength / 4},${center[1] - height - cuboidLength / 4} ${center[0] - cuboidWidth / 2 - cuboidLength / 4},${center[1] - height - cuboidLength / 4}`)
                                        .attr('fill', this.colorFunctionL(population))
                                        .attr('opacity', '0.6');

                                    // 绘制长方体的“左侧面”
                                    this.svg.append('polygon')
                                        .attr('points', `${center[0] - cuboidWidth / 2},${center[1]} ${center[0] - cuboidWidth / 2},${center[1] - height} ${center[0] - cuboidWidth / 2 - cuboidLength / 4},${center[1] - height - cuboidLength / 4} ${center[0] - cuboidWidth / 2 - cuboidLength / 4},${center[1] - cuboidLength / 4}`)
                                        .attr('fill', this.colorFunctionL(population))
                                        .attr('opacity', '0.9'); // 修改左侧面的颜色
                                }
                            }
                        });
                        if (this.ifDoubleEncoding == false) {
                            //draw legend
                            for (let i = 0, delta = 20, px = 50; i < 4; i++) {
                                let t = 1000000 * Math.pow(5, i), x = px;
                                let v = t / 800000;
                                let y = 330 - v;
                                this.svg.append('rect')
                                    .attr('x', px)
                                    .attr('y', 330 - v)
                                    .attr('width', 20)
                                    .attr('height', v)
                                    .attr('fill', 'rgba(230, 158, 165, 0.8)');
                                this.svg.append('polygon')
                                    .attr('points', `${x},${y} ${x - 8},${y - 8} ${x - 8},${y + v - 8} ${x},${y + v}`)
                                    .attr('fill', 'rgba(200, 60, 60, 0.5)');
                                this.svg.append('polygon')
                                    .attr('points', `${x},${y} ${x - 8},${y - 8} ${x + 12},${y - 8} ${x + 20},${y}`)
                                    .attr('fill', 'rgba(230, 158, 165, 0.6)');

                                const label = t < 1000 ? Math.floor(t) :
                                    t < 1000000 ? Math.floor(t / 1000) + "k" :
                                        Math.floor(t / 1000000) + "m";
                                this.svg.append('text')
                                    .attr('x', px - 5)
                                    .attr('y', 315 - v)
                                    .text(label);
                                px += 2 * delta;
                            }
                        } else {
                            //draw legend
                            for (let i = 0, delta = 20, px = 50; i < 4; i++) {
                                let t = 1000000 * Math.pow(5, i), x = px;
                                let v = t / 800000;
                                let y = 330 - v;
                                this.svg.append('rect')
                                    .attr('x', px)
                                    .attr('y', 330 - v)
                                    .attr('width', 20)
                                    .attr('height', v)
                                    .attr('fill', this.colorFunctionL(t))
                                    .attr('opacity', '0.8');
                                this.svg.append('polygon')
                                    .attr('points', `${x},${y} ${x - 8},${y - 8} ${x - 8},${y + v - 8} ${x},${y + v}`)
                                    .attr('fill', this.colorFunctionL(t))
                                    .attr('opacity', '0.9');
                                this.svg.append('polygon')
                                    .attr('points', `${x},${y} ${x - 8},${y - 8} ${x + 12},${y - 8} ${x + 20},${y}`)
                                    .attr('fill', this.colorFunctionL(t))
                                    .attr('opacity', '0.6');

                                const label = t < 1000 ? Math.floor(t) :
                                    t < 1000000 ? Math.floor(t / 1000) + "k" :
                                        Math.floor(t / 1000000) + "m";
                                this.svg.append('text')
                                    .attr('x', px - 5)
                                    .attr('y', 315 - v)
                                    .text(label);
                                px += 2 * delta;
                            }
                        }
                    }
                } else if (type === this.myType['2D Length']) {
                    d3.select("." + this.value + "-legend").selectAll("*").remove();
                    this.encodingChannelType = type;

                    this.encodingChannel = () => {
                        this.svg.selectAll('path').attr("fill", this.defaultColor);

                        // draw bar chart
                        const baseHeight = 3; // 长方体基础高度，所有长方体至少有这个高度
                        const populationPerHeight = 800000; // 每增加这么多人口，长方体的高度增加一单位
                        const cuboidWidth = 20; // 长方体的宽度

                        this.geoData.features.forEach(feature => {
                            const center = this.geoPath.centroid(feature);
                            const population = this.getPopulation(feature);
                            if (population >= 1000000) { // 人口大于等于1000000时绘制长方体
                                const height = baseHeight + (population / populationPerHeight); // 长方体的总高度

                                if (this.ifDoubleEncoding == false) {
                                    this.svg.append('rect')
                                        .attr('x', center[0] - cuboidWidth / 2)
                                        .attr('y', center[1] - height)
                                        .attr('width', cuboidWidth)
                                        .attr('height', height)
                                        .attr('fill', 'rgba(230, 158, 165, 0.7)');
                                } else {
                                    this.svg.append('rect')
                                        .attr('x', center[0] - cuboidWidth / 2)
                                        .attr('y', center[1] - height)
                                        .attr('width', cuboidWidth)
                                        .attr('height', height)
                                        .attr('fill', this.colorFunctionL(population))
                                        .attr('opacity', '0.7');
                                }
                            }
                        });
                        if (this.ifDoubleEncoding == false) {
                            //draw legend
                            for (let i = 0, delta = 20, px = 50; i < 4; i++) {
                                let t = 1000000 * Math.pow(5, i);
                                let v = t / 800000;
                                this.svg.append('rect')
                                    .attr('x', px)
                                    .attr('y', 330 - v)
                                    .attr('width', 20)
                                    .attr('height', v)
                                    .attr('fill', 'rgba(230, 158, 165, 0.7)');
                                const label = t < 1000 ? Math.floor(t) :
                                    t < 1000000 ? Math.floor(t / 1000) + "k" :
                                        Math.floor(t / 1000000) + "m";
                                this.svg.append('text')
                                    .attr('x', px)
                                    .attr('y', 320 - v)
                                    .text(label);
                                px += 2 * delta;
                            }
                        } else {
                            for (let i = 0, delta = 20, px = 50; i < 4; i++) {
                                let t = 1000000 * Math.pow(5, i);
                                let v = t / 800000;
                                this.svg.append('rect')
                                    .attr('x', px)
                                    .attr('y', 330 - v)
                                    .attr('width', 20)
                                    .attr('height', v)
                                    .attr('fill', this.colorFunctionL(t))
                                    .attr('opacity', '0.7');
                                const label = t < 1000 ? Math.floor(t) :
                                    t < 1000000 ? Math.floor(t / 1000) + "k" :
                                        Math.floor(t / 1000000) + "m";
                                this.svg.append('text')
                                    .attr('x', px)
                                    .attr('y', 320 - v)
                                    .text(label);
                                px += 2 * delta;
                            }
                        }
                    }
                }


                // Encoding Size
                else if (type === this.myType['Size']) {
                    d3.select("." + this.value + "-legend").selectAll("*").remove();
                    this.encodingChannelType = type;

                    this.encodingChannel = () => {
                        this.svg.selectAll('path').attr("fill", this.defaultColor);

                        // 在地图上绘制人口方块
                        // this.drawPopulationSquares();
                        const populationExtent = d3.extent(this.geoData.features, d => this.getPopulation(d));
                        const sizeScale = d3.scaleSqrt()
                            .domain(populationExtent)
                            .range([5, 50]); // 方块大小的范围

                        // 直接在现有的SVG上绘制方块，不清除之前的内容
                        this.geoData.features.forEach(feature => {
                            const [x, y] = this.geoPath.centroid(feature);
                            const population = this.getPopulation(feature);
                            if (population >= 1000000) { // 人口大于等于1000000时绘制方块
                                if (this.ifDoubleEncoding == false) {
                                    this.svg.append('rect')
                                        .attr('x', x - sizeScale(population) / 2)
                                        .attr('y', y - sizeScale(population) / 2)
                                        .attr('width', sizeScale(population))
                                        .attr('height', sizeScale(population))
                                        .attr('fill', 'rgba(230, 158, 165, 0.7)');
                                } else {
                                    this.svg.append('rect')
                                        .attr('x', x - sizeScale(population) / 2)
                                        .attr('y', y - sizeScale(population) / 2)
                                        .attr('width', sizeScale(population))
                                        .attr('height', sizeScale(population))
                                        .attr('fill', this.colorFunctionL(population))
                                        .attr('opacity', '0.7');
                                }

                            }
                        });
                        if (this.ifDoubleEncoding == false) {
                            //draw size legend
                            for (let i = 0, delta = 20, py = 100; i < 4; i++) {
                                let t = 1000000 * Math.pow(5, i)
                                let v = sizeScale(t);
                                this.svg.append('rect')
                                    .attr('x', 50)
                                    .attr('y', py)
                                    .attr('width', v)
                                    .attr('height', v)
                                    .attr('fill', 'rgba(230, 158, 165, 0.7)');

                                const label = t < 1000 ? Math.floor(t) :
                                    t < 1000000 ? Math.floor(t / 1000) + "k" :
                                        Math.floor(t / 1000000) + "m";
                                this.svg.append('text')
                                    .attr('x', 65 + v)
                                    .attr('y', py + v)
                                    .text(label);

                                py += v + delta;
                            }
                        } else {
                            for (let i = 0, delta = 20, py = 100; i < 4; i++) {
                                let t = 1000000 * Math.pow(5, i)
                                let v = sizeScale(t);
                                this.svg.append('rect')
                                    .attr('x', 50)
                                    .attr('y', py)
                                    .attr('width', v)
                                    .attr('height', v)
                                    .attr('fill', this.colorFunctionL(t))
                                    .attr('opacity', '0.7');

                                const label = t < 1000 ? Math.floor(t) :
                                    t < 1000000 ? Math.floor(t / 1000) + "k" :
                                        Math.floor(t / 1000000) + "m";
                                this.svg.append('text')
                                    .attr('x', 65 + v)
                                    .attr('y', py + v)
                                    .text(label);

                                py += v + delta;
                            }
                        }
                    }
                }

                //Encoding Quantity
                else if (type === this.myType['Quantity']) {
                    this.encodingChannelType = type;

                    this.encodingChannel = () => {
                        this.svg.selectAll('path').attr("fill", this.defaultColor);

                        // 在地图上叠加人口图标
                        const iconWidth = 10; // 图标的宽度
                        const iconHeight = 25; // 图标的高度
                        const iconGap = 3; // 调整图标间的间隔
                        const scaleX = 0.4;
                        const scaleY = 0.4;

                        // 直接在现有的SVG上绘制图标，不清除之前的内容
                        this.geoData.features.forEach(feature => {
                            const center = this.geoPath.centroid(feature);
                            const population = this.getPopulation(feature);

                            // 只有当人口大于等于1000000时才绘制图标
                            if (population >= 1000000) {
                                const totalIcons = Math.ceil(population / 8000000); // 总图标数

                                for (let i = 0; i < totalIcons; i++) {
                                    // 计算图标的位置
                                    // 将图标排列成一行显示5个图标的形式
                                    const x = center[0] - ((iconWidth + iconGap) * 5 / 2) + ((i % 5) * (iconWidth + iconGap));
                                    const y = center[1] + (Math.floor(i / 5) * (iconHeight + iconGap)) - 10;
                                    const x1 = x + 6.5;
                                    const y1 = y - 3.5;
                                    // 添加图标
                                    if (this.ifDoubleEncoding == false) {
                                        // this.svg.append('image')
                                        // .attr('xlink:href', require('../assets/PersonIcon.svg')) // 图标的路径
                                        // .attr('x', x)
                                        // .attr('y', y)
                                        // .attr('width', iconWidth)
                                        // .attr('height', iconHeight)
                                        // .attr('opcacity', 0.7);
                                        var g = this.svg.append('g');
                                        g.append('path')
                                            .attr('d', "M1 14.0338C1 10.5338 1 7.5338 4.5 4.0338C7.3 1.2338 12 0.867135 14 1.0338L19.5 1.03381C21.5 1.03381 26.2 1.6338 29 4.0338C31.8 6.4338 32.1667 11.7005 32 14.0338V24.0338C32 26.8338 28.3333 28.8671 26.5 29.5338L24.5 42.0338C24.5 43.2338 23.1667 44.2005 22.5 44.5338H10.5C9.7 44.5338 9.16667 42.8671 9 42.0338L7 29.5338C4.2 29.9338 2.16667 26.0338 1.5 24.0338C1.33333 21.8671 1 16.8338 1 14.0338Z")
                                            .attr('transform', 'scale(' + scaleX + ',' + scaleY + ')')
                                            .attr('fill', 'rgba(230, 158, 165, 0.7)')
                                            .attr('stroke', 'none')
                                            .attr('stroke-width', 3);
                                        this.svg.append('circle')
                                            .attr('cx', x1)
                                            .attr('cy', y1)
                                            .attr('r', 4)
                                            .style('stroke', 'none')
                                            .style('fill', 'rgba(230, 158, 165, 0.7)');
                                        g.attr('transform', 'translate(' + x + ',' + y + ')')
                                            .attr('transform', 'scale(' + scaleX + ',' + scaleY + ')')
                                            .attr('fill', 'rgba(230, 158, 165, 0.7)')
                                            .attr('stroke', 'none')
                                            .attr('stroke-width', 3);
                                        g.attr('transform', 'translate(' + x + ',' + y + ')');
                                    } else {
                                        // var gg = this.svg.append('g');
                                        // gg.append('path')
                                        //     .attr('d', 'M14.8025 62.0243H13.3025V63.5243V109.33C13.3025 112.457 10.7652 114.995 7.62974 114.995C4.52341 114.995 2.05603 112.482 2.05603 109.33V58.5276C2.05603 47.7847 10.8631 39.0498 21.6399 39.0498H57.8253C68.5917 39.0498 77.4056 47.7849 77.4056 58.5276V109.33C77.4056 112.483 74.9364 114.995 71.8267 114.995C68.6982 114.995 66.1557 112.454 66.1557 109.33V63.5243V62.0243H64.6557H60.9589H59.4589V63.5243V190.975C59.4589 195.441 55.8001 199.086 51.3147 199.086C46.8293 199.086 43.2017 195.448 43.2017 190.975V116.968V115.468H41.7017H37.7564H36.2564V116.968V190.975C36.2564 195.449 32.6278 199.086 28.1539 199.086C23.6745 199.086 20.0392 195.447 20.0392 190.975C20.0392 187.046 20.0184 155.183 19.9975 124.302C19.9871 108.862 19.9767 93.6674 19.9689 82.3327L19.9594 68.6775L19.9568 64.8683L19.9561 63.8666L19.9559 63.61L19.9558 63.5451V63.5288V63.5247C19.9558 63.5238 19.9558 63.5233 18.4558 63.5243L19.9558 63.5233L19.9548 62.0243H18.4558H14.8025ZM39.7326 31.8474C31.5119 31.8474 24.8553 25.1836 24.8535 16.9684C24.8537 8.74658 31.5101 2.08571 39.7326 2.08571C47.945 2.08571 54.6081 8.74501 54.6081 16.9684C54.6081 25.1831 47.945 31.8474 39.7326 31.8474Z')
                                        //     .attr('transform', 'scale(' + scaleX + ',' + scaleY + ')')
                                        //     .attr('fill', this.colorFunctionL(population))
                                        //     .attr('stroke', 'black')
                                        //     .attr('stroke-width', 3);
                                        // gg.attr('transform', 'translate(' + x + ',' + y + ')');
                                        var gd = this.svg.append('g');
                                        gd.append('path')
                                            .attr('d', "M1 14.0338C1 10.5338 1 7.5338 4.5 4.0338C7.3 1.2338 12 0.867135 14 1.0338L19.5 1.03381C21.5 1.03381 26.2 1.6338 29 4.0338C31.8 6.4338 32.1667 11.7005 32 14.0338V24.0338C32 26.8338 28.3333 28.8671 26.5 29.5338L24.5 42.0338C24.5 43.2338 23.1667 44.2005 22.5 44.5338H10.5C9.7 44.5338 9.16667 42.8671 9 42.0338L7 29.5338C4.2 29.9338 2.16667 26.0338 1.5 24.0338C1.33333 21.8671 1 16.8338 1 14.0338Z")
                                            .attr('transform', 'scale(' + scaleX + ',' + scaleY + ')')
                                            .attr('fill', this.colorFunctionL(population))
                                            .attr('stroke', 'none')
                                            .attr('stroke-width', 3);
                                        this.svg.append('circle')
                                            .attr('cx', x1)
                                            .attr('cy', y1)
                                            .attr('r', 3)
                                            .style('stroke', 'none')
                                            .style('fill', this.colorFunctionL(population));
                                        gd.attr('transform', 'translate(' + x + ',' + y + ')')
                                            .attr('transform', 'scale(' + scaleX + ',' + scaleY + ')')
                                            .attr('fill', this.colorFunctionL(population))
                                            .attr('stroke', 'none')
                                            .attr('stroke-width', 3);
                                        gd.attr('transform', 'translate(' + x + ',' + y + ')');
                                    }
                                }
                            }
                        });
                        //draw quantity legend
                        this.svg.append('image')
                            .attr('xlink:href', require('../assets/PersonIcon.svg')) // 图标的路径
                            .attr('x', 50)
                            .attr('y', 100)
                            .attr('width', iconWidth * 2)
                            .attr('height', iconHeight * 2);
                        this.svg.append('text')
                            .attr('x', 70)
                            .attr('y', 120)
                            .text(':100k');
                        if (this.ifDoubleEncoding == true) {
                            if (this.preColortype == 0) {
                                //luminance legend
                                this.drawColorLuminanceLegend();
                            } else if (this.preColortype == 1) {
                                //hue legend
                                this.drawColorHueLegend();
                            }
                        }
                        
                    }


                } else if (type === this.myType['Remove']) {
                    this.encodingChannelType = type;

                    this.encodingChannel = () => {
                        this.svg.selectAll('path').attr("fill", this.defaultColor);
                        d3.select("." + this.value + "-legend").selectAll("*").remove();
                    }
                } else {
                    // // 如果没有适用的编码方式
                    // this.encodingChannelType = -1; // 或其他表示无效编码方式的值

                    // // 显示一条消息
                    // this.encodingChannel = () => {
                    //     this.svg.selectAll('path').attr("fill", this.defaultColor);

                    //     // 首先，清除可能存在的旧消息
                    //     d3.select("." + this.value + "-legend").selectAll("*").remove();

                    //     // 向legend SVG元素中添加文本
                    //     d3.select("." + this.value + "-legend")
                    //         .append('text')
                    //         .attr('x', 10) // 根据需要调整文本的x位置
                    //         .attr('y', 20) // 根据需要调整文本的y位置
                    //         .attr('fill', 'black') // 文本颜色
                    //         .style('font-size', '14px') // 文本大小
                    //         .text('This encoding method is not applicable to the current data provided.');
                    // };
                    // d3.select("." + this.value + "-legend").selectAll("*").remove();
                    this.showErrorDialog("Encoding Channel Not Support", "The selected encoding channel only support the data your uploaded!")
                }
            } else {
                d3.select("." + this.value + "-legend").selectAll("*").remove();
                if (type === this.myType['Glyph']) {
                    this.encodingChannelType = type;
                    this.encodingChannel = () => {
                        this.svg.selectAll('path').attr("fill", this.defaultColor);

                        this.geoData.features.forEach(feature => {
                            const flagBase64 = this.getPopulation(feature); // 使用getPopulation方法尝试从infoData获取国旗的base64编码

                            // 检查flagBase64是否不等于-1，仅当不等于-1时，才显示国旗
                            if (flagBase64 !== -1) {
                                const center = this.geoPath.centroid(feature); // 计算国家地理中心点

                                // 在地图的国家中心点上添加国旗图像
                                if (this.ifDoubleEncoding == false) {
                                    this.svg.append('image')
                                        .attr('xlink:href', flagBase64) // 使用国旗的base64编码
                                        .attr('x', center[0] - 10) // 你可能需要调整这个以适合国旗图像的大小和位置
                                        .attr('y', center[1] - 10) // 同上
                                        .attr('width', 20) // 根据需要调整国旗的尺寸
                                        .attr('height', 20);
                                } else {
                                    this.svg.append('image')
                                        .attr('xlink:href', flagBase64) // 使用国旗的base64编码
                                        .attr('x', center[0] - 10) // 你可能需要调整这个以适合国旗图像的大小和位置
                                        .attr('y', center[1] - 10) // 同上
                                        .attr('width', 20) // 根据需要调整国旗的尺寸
                                        .attr('height', 20)
                                        .attr('fill', this.colorFunctionL());
                                }

                            }
                        });
                    };
                } else if (type === this.myType['Color (Hue)']) {
                    this.encodingChannelType = type;

                    // 1. 创建一个包含所有国家名称的数组
                    const countries = this.geoData.features.map(d => d.properties.NAME);

                    // 2. 自定义一个包含51种颜色的数组
                    const customColors = [
                        "#e6194B", "#3cb44b", "#ffe119", "#4363d8", "#f58231", "#911eb4", "#46f0f0", "#f032e6",
                        "#bcf60c", "#fabebe", "#008080", "#e6beff", "#9a6324", "#fffac8", "#800000", "#aaffc3",
                        "#808000", "#ffd8b1", "#000075", "#808080", "#123123", "#000000",
                        // 添加更多颜色以确保有51种不同的颜色
                        "#59656d", "#c17b81", "#b5d99c", "#f5b971", "#8fb5aa", "#f28a9b", "#a4c3ed", "#8ec6c5",
                        "#c6d7eb", "#ead3c1", "#92b4a7", "#f4ebc1", "#cbb3bf", "#acb7ae", "#e2c2de", "#cccccc",
                        "#b97a57", "#ab69c6", "#966fd6", "#cfcfc4", "#b39eb5", "#779ecb", "#fdfd96", "#836953",
                        "#779ecb", "#03c03c", "#966fd6", "#c23b22", "#f49ac2", "#fadadd"
                    ];

                    // 使用d3.scaleOrdinal来映射国家到颜色
                    const colorScale = (d) => {
                        if (d && d.properties && d.properties.NAME)
                            return d3.scaleOrdinal(countries, customColors)(d.properties.NAME);
                        else
                            return this.defaultColor;
                    }

                    // 重写encodingChannel函数
                    this.encodingChannel = () => {
                        // 在地图上为每个国家应用颜色
                        this.svg.selectAll('path')
                            .attr('fill', d => colorScale(d)) // 使用比例尺确定颜色
                            .attr('stroke', '#ffffff'); // 设置边框颜色，可根据需要调整

                        this.svg.selectAll('circle')
                            .attr('fill', d => colorScale(d))
                            .attr('stroke', '#ffffff');
                        this.highLights[this.pointer2highlight].forEach(highLight => {
                            highLight();
                        });
                    };
                } else {
                    // // 如果没有适用的编码方式
                    // this.encodingChannelType = -1; // 或其他表示无效编码方式的值

                    // // 显示一条消息
                    // this.encodingChannel = () => {
                    //     this.svg.selectAll('path').attr("fill", this.defaultColor);

                    //     // 首先，清除可能存在的旧消息
                    //     d3.select("." + this.value + "-legend").selectAll("*").remove();

                    //     // 向legend SVG元素中添加文本
                    //     d3.select("." + this.value + "-legend")
                    //         .append('text')
                    //         .attr('x', 10) // 根据需要调整文本的x位置
                    //         .attr('y', 20) // 根据需要调整文本的y位置
                    //         .attr('fill', 'black') // 文本颜色
                    //         .style('font-size', '14px') // 文本大小
                    //         .text('This encoding method is not applicable to the current data provided.');
                    // };

                    this.showErrorDialog("Encoding Channel Not Support", "The selected encoding channel only support the data your uploaded!")
                }


            }


            this.drawSvg();
        },

        drawColorLuminanceLegend() {
            const legendWidth = this.legendWidth;
            const legendHeight = 20;
            const numSegments = 8; // 将色彩标尺等分成5段

            const segmentWidth = legendWidth / numSegments; // 每个段的宽度
            const populationWidth = Math.pow(this.mostPopulation, 0.25) / numSegments

            const legendGradient = this.legend.append('svg')
                .attr('width', legendWidth)
                .attr('height', legendHeight);

            this.legend.append('text')
                .attr('x', 0)
                .attr('y', legendHeight + 15)
                // .attr('text-anchor', 'middle')
                .text('0')
                .style('font-size', '10px');

            // 绘制每个段的渐变色块和白色分隔线
            for (let i = 0; i < numSegments; i++) {
                const segmentStart = i * segmentWidth;
                const segmentEnd = (i + 1) * segmentWidth;

                const populationStart = Math.pow(i * populationWidth, 4);
                const populationEnd = Math.pow((i + 1) * populationWidth, 4);

                // 添加渐变色块
                const gradient = legendGradient.append('defs')
                    .append('linearGradient')
                    .attr('id', `legendGradient${i}`)
                    .attr('x1', '0%')
                    .attr('y1', '0%')
                    .attr('x2', '100%')
                    .attr('y2', '0%');

                gradient.append('stop')
                    .attr('offset', '0%')
                    .attr('stop-color', this.colorFunctionL(populationStart));

                gradient.append('stop')
                    .attr('offset', '100%')
                    .attr('stop-color', this.colorFunctionL(populationEnd));

                // 绘制渐变色块
                legendGradient.append('rect')
                    .attr('x', segmentStart)
                    .attr('y', 0)
                    .attr('width', segmentWidth)
                    .attr('height', legendHeight)
                    .style('fill', `url(#legendGradient${i})`);

                // 添加白色分隔线
                if (i < numSegments - 1) {
                    legendGradient.append('line')
                        .attr('x1', segmentEnd)
                        .attr('y1', 0)
                        .attr('x2', segmentEnd)
                        .attr('y2', legendHeight)
                        .style('stroke', '#ffffff')
                        .style('stroke-width', 1);
                }

                // 添加数值标签
                const label = populationEnd < 1000 ? Math.floor(populationEnd) :
                    populationEnd < 1000000 ? Math.floor(populationEnd / 1000) + "k" :
                        Math.floor(populationEnd / 1000000) + "m"
                this.legend.append('text')
                    .attr('x', segmentEnd)
                    .attr('y', legendHeight + 15)
                    .attr('text-anchor', 'middle')
                    .text(label)
                    .style('font-size', '10px');
            }
        },

        drawColorHueLegend() {
            const legendData = [
                {color: 'rgb(142, 207, 201)', text: '< 5M', minPopulation: 0, maxPopulation: 5000000},
                {color: 'rgb(255, 190, 122)', text: '5M-10M', minPopulation: 5000000, maxPopulation: 10000000},
                {color: 'rgb(250, 127, 111)', text: '10M-50M', minPopulation: 10000000, maxPopulation: 50000000},
                {color: 'rgb(130, 176, 210)', text: '50M-100M', minPopulation: 50000000, maxPopulation: 100000000},
                {color: 'rgb(190, 184, 220)', text: '>100M', minPopulation: 100000000, maxPopulation: Infinity}
            ];

            const legendWidth = 20;
            const legendHeight = 20;
            const legendSpacing = 10;
            const legendX = 10; // Starting x position for the legend
            const legendY = 10; // Starting y position for the legend

            // Create a group for the legend
            // const legend = this.svg.append('g')
            //     .attr('class', 'legend')
            //     .attr('transform', `translate(${legendX},${legendY})`);

            this.legend.append('g')
                .attr('class', 'legend')
                .attr('transform', `translate(${legendX},${legendY})`);

            // Add color swatches
            this.legend.selectAll('rect')
                .data(legendData)
                .enter().append('rect')
                .attr('x', (d, i) => i * (legendHeight + legendSpacing) * 2)
                .attr('y', 0)
                .attr('width', legendWidth)
                .attr('height', legendHeight)
                .style('fill', d => d.color);

            // Add text labels
            this.legend.selectAll('text')
                .data(legendData)
                .enter().append('text')
                .attr('x', (d, i) => i * (legendHeight + legendSpacing) * 2)
                .attr('y', legendWidth + 5)
                .attr('dy', '.35em') // Vertically center
                .style('font-size', '10px')
                .text(d => d.text);
        },

        doubleEncoding() {
            this.ifDoubleEncoding = !this.ifDoubleEncoding;
            this.ifDoubleEncodingText = this.ifDoubleEncoding ? 'Dual Encoding: ON' : 'Dual Encoding: OFF';
            if (this.ifDoubleEncoding)
                alert('Attention! Only supporting for one color method with one length, size or quantity method.');
        },

        printSVG() {
            var tempsvg = this.svg;
            tempsvg.selectAll('*')
                .attr('transform', 'translate(0, 10)');
            var legendItems = this.legend.selectAll('*');

            // 将图形移植到 tempsvg 上
            legendItems.each(function () {
                tempsvg.node().appendChild(this);
            });
            // 选择包含图形的SVG元素
            tempsvg.selectAll('*')
                .attr('transform', 'translate(10, 10)');
            var svgElement = tempsvg.node();

            // 将SVG内容转换为字符串
            var svgString = new XMLSerializer().serializeToString(svgElement);

            // 创建Blob对象
            var blob = new Blob([svgString], {type: 'image/svg+xml'});

            // 创建URL
            var url = window.URL.createObjectURL(blob);

            // 创建一个a标签用于下载
            var a = document.createElement('a');
            a.href = url;
            a.download = 'd3_chart.svg'; // 下载文件的名称

            // 模拟点击链接以触发下载
            document.body.appendChild(a);
            a.click();

            // 清除之前创建的URL对象
            window.URL.revokeObjectURL(url);

        },
        getTextWidth(text, fontSize) {
            let canvas = document.createElement('canvas');
            let context = canvas.getContext('2d');
            context.font = fontSize + ' sans-serif';
            return context.measureText(text).width;
        }
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

.row-with-line {
    position: relative; /* 设置相对定位，以便将竖线定位相对于该行 */
}

.row-with-line::before {
    content: '';
    width: 3px; /* 竖线的宽度 */
    height: 90%; /* 竖线的高度*/
    background-color: pink; /* 竖线的颜色 */
    position: absolute; /* 使竖线定位在行的左侧 */
    left: 0; /* 将竖线定位在行的左侧 */
    top: 0; /* 将竖线定位在行的顶部 */
}

#myButton {
    border: 2px solid transparent; /* 设置默认的边框，透明色 */
    outline: none; /* 取消浏览器默认的焦点轮廓 */
    /* border-color: pink; */
}

#myButton:hover {
    border-color: pink; /* 设置选中时的边框颜色为粉色 */
    /*outline: none;      /* 取消浏览器默认的焦点轮廓 */
}

.matched-heading {
    background-color: pink;
    padding: 10px;
    text-align: center;
}

.colorfulButton {
    background-color: pink; /* 设置按钮的背景颜色为红色 */
    color: #000000; /* 设置按钮文字颜色为白色 */
    border-radius: 5px;
}

.button-row {
    margin-bottom: 2px; /* 添加20像素的底部间距 */
}

</style>