<template>
    <v-container>
        <v-row>
            <h1>About</h1>
        </v-row>
        <v-row>
            <v-col>
                <v-img :src="require('../assets/MapCraftUsageFlowChart.png')" contain/>
            </v-col>
        </v-row>

        <v-row>
            <v-col>
                <v-img :src="require('../assets/AuthoringInterface.png')" contain/>
            </v-col>
        </v-row>

        <v-row>
            <div class="row-with-line"></div>
            <v-col>
                <div class="text">
                    The interface is thoughtfully divided into two principal components: the Components Panel and the Canvas Panel, facilitating an organized and intuitive approach to geo-infographic creation.
                </div> 
            </v-col>
              
        </v-row>
        <v-row>
            <div class="row-with-line"></div>
            <v-col>
                <div class="text">
                    Inside the Components Panel, there is a curated selection of visual elements, categorized according to a design space framework that encompasses four pivotal dimensions of geo-infographic design.
                </div>
            </v-col>
            
        </v-row>
        <v-row>
            <div class="row-with-line"></div>
            <v-col>
                <div class="text">
                    Users may select the visual elements of choice from the Components Panel for each dimension. The data designated for encoding, signified by the second key-value pair within the JSON file, is integrated into the encoding channel. Country names listed in the JSON file serve to align the data with corresponding labels and their designated positions on the map. The optional labels included in the JSON file can be strategically positioned as per the user's selected design preferences.
                </div>
            </v-col>
        </v-row>
        <v-row>
            <div class="row-with-line"></div>
            <v-col>
                <div class="text">
                    It should be highlighted that the components within the dimensions of Basic Map Representations and Label Design and Placement are mutually exclusive, implying that only one type of component can be active within each dimension at any given time.
                </div>
            </v-col>
            
        </v-row>
        <v-row>
            <div class="row-with-line"></div>
            <v-col>
                <div class="text">
                    An advanced functionality of the interface is the 'dual encoding' button, which empowers users to implement dual encoding by selecting elements from two encoding channels concurrently. This feature allows for a more nuanced representation of data. Furthermore, all highlighting techniques within the Highlighting Techniques dimension are versatile and can be applied in multiples, with no restrictions on the number of uses.
                </div>
            </v-col>
        </v-row>
        <v-row>
            <div class="row-with-line"></div>
            <v-col>
            <div class="text">
                The Canvas Panel acts as the central workspace where users can assemble their geo-infographics. Upon finalizing the composition, users can export the geo-infographic as an SVG file by utilizing the 'print' button, encapsulating their work on the Canvas Panel.
            </div>
            </v-col>
            
        </v-row>

    </v-container>
</template>

<script>

export default {
    name: 'aboutTab',

    data() {
        return {
        };
    },
    methods: {
    },
}
</script>

<style scoped>
h1 {
    font-size: 56px;
}

.text{
    margin: 10px;
}

.row-with-line {
    position: relative; /* 设置相对定位，以便将竖线定位相对于该行 */
}

.row-with-line::before {
    content: '';
    width: 6px; /* 竖线的宽度 */
    height: 90%; /* 竖线的高度*/
    background-color: pink; /* 竖线的颜色 */
    position: absolute; /* 使竖线定位在行的左侧 */
    left: 0; /* 将竖线定位在行的左侧 */
    top: 0; /* 将竖线定位在行的顶部 */
}
</style>