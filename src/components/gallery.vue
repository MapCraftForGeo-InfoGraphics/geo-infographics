<template>
    <div style=" height: 100%; width: 100%;">
        <v-container style="margin: 5; height: 100%; width: 100%;">
            <v-row>
                <v-col>
                    <h2>Quantitative</h2>
                </v-col>
                <v-col>
                    <h2>Categorical</h2>
                </v-col>
            </v-row>
            
            <v-row>
                <v-col class="image-with-text">
                    <v-img :src="require('../assets/galleryZhaoC.png')" contain/>
                </v-col>
                <v-col class="image-with-text">
                    <v-img :src="require('../assets/galleryZhaoP.png')" contain/>
                </v-col>
            </v-row>
            <v-row>
                <v-col>
                    <div  class="text-container">
                        <div>Basic Map: Topographic Map</div>
                        <div>Encoding Channel: Quantity</div>
                        <div>Label Position: Icon</div>
                        <div>Highlight: Light, Map Pin, Enlarged Portions</div>
                    </div>
                </v-col>
                <v-col>
                    <div  class="text-container">
                        <div>Basic Map: Political Map</div>
                        <div>Encoding Channel: Color Hue</div>
                        <div>Label Position: Convenient</div>
                        <div>Highlight: Contour, Map Pin, 3D Transformation, Enlarged Portions</div>
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

</style>