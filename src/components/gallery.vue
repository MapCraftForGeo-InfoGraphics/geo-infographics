<template>
    <div style=" height: 100%; width: 100%;">
        <v-container style="margin: 5; height: 100%; width: 100%;">
            <v-row>
                <div class="row-with-line"></div>
                <v-col style="padding: 0;">
                    <h2 class="matched-heading">Quantitative</h2>
                </v-col>
                <div class="row-with-line"></div>
                <v-col style="padding: 0;">
                    <h2 class="matched-heading">Categorical</h2>
                </v-col>
            </v-row>

            <v-row>
                <div class="row-with-line"></div>
                <v-col class="image-with-text">
                    <v-img :src="require('../assets/gallery4P.png')" contain/>
                </v-col>
                <div class="row-with-line"></div>
                <v-col class="image-with-text">
                    <v-img :src="require('../assets/gallery5C.png')" contain/>
                </v-col>
            </v-row>
            <v-row>
                <div class="row-with-line"></div>
                <v-col>
                    <div  class="text-container">
                        <div>Basic Map: Political Map</div>
                        <div>Encoding Channel: Color Hue, Quantity</div>
                        <div>Label Position: Color</div>
                        <div>Highlight: Contour, Enlarged Portions</div>
                    </div>
                </v-col>
                <div class="row-with-line"></div>
                <v-col>
                    <div  class="text-container">
                        <div>Basic Map: Political Map</div>
                        <div>Encoding Channel: Glyph</div>
                        <div>Label Position: Color</div>
                        <div>Highlight: Contour, Map Pin, Light, Enlarged Portions</div>
                    </div>
                </v-col>
            </v-row>
            

            <v-row>
                <div class="row-with-line"></div>
                <v-col class="image-with-text">
                    <v-img :src="require('../assets/gallery3P.png')" contain/>
                </v-col>
                <div class="row-with-line"></div>
                <v-col class="image-with-text">
                    <v-img :src="require('../assets/galleryZhaoC.png')" contain/>
                </v-col>
            </v-row>
            <v-row>
                <div class="row-with-line"></div>
                <v-col>
                    <div  class="text-container">
                        <div>Basic Map: Political Map</div>
                        <div>Encoding Channel: Color Intensity</div>
                        <div>Label Position: Aligned</div>
                        <div>Highlight: Light, Map Pin</div>
                    </div>
                </v-col>
                <div class="row-with-line"></div>
                <v-col>
                    <div  class="text-container">
                        <div>Basic Map: Political Map</div>
                        <div>Encoding Channel: Color Hue</div>
                        <div>Label Position: Convenient</div>
                        <div>Highlight: Map Pin, Enlarged Portions</div>
                    </div>
                </v-col>
            </v-row>

            <v-row>
                <div class="row-with-line"></div>
                <v-col class="image-with-text">
                    <v-img :src="require('../assets/galleryZhaoP.png')" contain/>
                </v-col>
                <div class="row-with-line"></div>
                <v-col class="image-with-text">
                    <v-img :src="require('../assets/gallery4C.png')" contain/>
                </v-col>
            </v-row>
            <v-row>
                <div class="row-with-line"></div>
                <v-col>
                    <div  class="text-container">
                        <div>Basic Map: Topographic Map</div>
                        <div>Encoding Channel: Quantity, Icon</div>
                        <div>Label Position: Icon</div>
                        <div>Highlight: Light, Map Pin, Enlarged Portions</div>
                    </div>
                </v-col>
                <div class="row-with-line"></div>
                <v-col>
                    <div  class="text-container">
                        <div>Basic Map: Topographic Map</div>
                        <div>Encoding Channel: Glyph</div>
                        <div>Label Position: Aligned</div>
                        <div>Highlight: Map Pin, Enlarged Portions</div>
                    </div>
                </v-col>
            </v-row>

            <v-row>
                <div class="row-with-line"></div>
                <v-col class="image-with-text">
                    <v-img :src="require('../assets/gallery5P.png')" contain/>
                </v-col>
                <div class="row-with-line"></div>
                <v-col class="image-with-text">
                    <v-img :src="require('../assets/gallery3C.png')" contain/>
                </v-col>
            </v-row>
            <v-row>
                <div class="row-with-line"></div>
                <v-col>
                    <div  class="text-container">
                        <div>Basic Map: Shape-based Map</div>
                        <div>Encoding Channel: Color Hue</div>
                        <div>Label Position: Icon</div>
                        <div>Highlight: Map Pin, Light</div>
                    </div>
                </v-col>
                <div class="row-with-line"></div>
                <v-col>
                    <div  class="text-container">
                        <div>Basic Map: Political Map</div>
                        <div>Encoding Channel: Glyph</div>
                        <div>Label Position: Convenient</div>
                        <div>Highlight: Color, Contour, Enlarged Portions</div>
                    </div>
                </v-col>
            </v-row>

            
        </v-container>
    </div>
    
</template>

<script>

export default {
    name: 'galleryTab',

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
.image-with-text {
    display: flex;
    /* align-items: center; 垂直居中对齐 */
}

.text-container {
    margin-left: 20px; /* 调整文字与图片之间的距离 */
    word-wrap: break-word; /* 或者 overflow-wrap: break-word; */
}

.row-with-line {
    position: relative; /* 设置相对定位，以便将竖线定位相对于该行 */
}

.row-with-line::before {
    content: '';
    width: 3px; /* 竖线的宽度 */
    height: 100%; /* 竖线的高度*/
    background-color: pink; /* 竖线的颜色 */
    position: absolute; /* 使竖线定位在行的左侧 */
    left: 0; /* 将竖线定位在行的左侧 */
    top: 0; /* 将竖线定位在行的顶部 */
}

.matched-heading {
    background-color: pink;
    padding: 10px;
    text-align: center;
    width: 95%;
}

</style>