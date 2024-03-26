<template>
    <v-expansion-panels>
        <v-expansion-panel>
            <v-expansion-panel-title>
                Basic Map Representations
            </v-expansion-panel-title>

            <v-expansion-panel-text>
                <v-container class="container">
                    <v-row>
                        <v-col class="element">
                            Political Map
                            <v-img :src="require('../assets/PoliticalMap.svg')" contain/>
                        </v-col>

                        <v-col class="element">
                            Topographic Map
                            <v-img :src="require('../assets/TopographicMap.svg')" contain/>
                        </v-col>
                    </v-row>

                    <v-row>
                        <v-col class="element">
                            Shape-based Map
                            <v-img :src="require('../assets/Shape-basedMap.svg')" contain/>
                        </v-col>

                        <v-col class="element">
                            Street Map
                            <v-img :src="require('../assets/StreetMap.svg')" contain/>
                        </v-col>
                    </v-row>

                    <v-row>
                        <v-col class="element">
                            Grid Cartogram
                            <v-img :src="require('../assets/GridCartogram.svg')" contain/>
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
                        <v-col class="element">
                            Mollweide
                            <v-img :src="require('../assets/Mollweide.svg')" contain/>
                        </v-col>

                        <v-col class="element">
                            Robinson
                            <v-img :src="require('../assets/Robinson.svg')" contain/>
                        </v-col>
                    </v-row>
                </v-container>
            </v-expansion-panel-text>
        </v-expansion-panel>


        <v-expansion-panel>
            <v-expansion-panel-title>
                Hightlight Techniques
            </v-expansion-panel-title>

            <v-expansion-panel-text>
                <v-container class="container">
                    <v-row>
                        <v-col class="element">
                            Light
                            <v-img :src="require('../assets/HighlightLight.svg')" contain/>
                        </v-col>

                        <v-col class="element">
                            Robinson
                            <v-img :src="require('../assets/HighlightColor.svg')" contain/>
                        </v-col>
                    </v-row>

                    <v-row>
                        <v-col class="element">
                            Color
                            <v-img :src="require('../assets/HighlightMappin.svg')" contain/>
                        </v-col>

                        <v-col class="element">
                            Mollweide
                            <v-img :src="require('../assets/Highlight3d.svg')" contain/>
                        </v-col>
                    </v-row>

                    <v-row>
                        <v-col class="element">
                            Enlarger
                            <v-img :src="require('../assets/HighlightEnlarge.svg')" width="61%" contain/>
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
                            <v-col class="element">
                                Situated
                                <v-img :src="require('../assets/Situated.svg')" contain/>
                            </v-col>

                            <v-col></v-col>
                        </v-row>
                    </v-container>

                    <div class="sub-title">Matched</div>
                    <v-container class="sub-container">
                        <v-row>
                            <v-col class="element">
                                Text
                                <v-img :src="require('../assets/MatchedText.svg')" contain/>
                            </v-col>

                            <v-col class="element">
                                Icon
                                <v-img :src="require('../assets/MatchedIcon.svg')" contain/>
                            </v-col>
                        </v-row>

                        <v-row>
                            <v-col class="element">
                                Color
                                <v-img :src="require('../assets/MathchedColor.svg')" contain/>
                            </v-col>
                            <v-col></v-col>
                        </v-row>
                    </v-container>

                    <div class="sub-title">Linked</div>
                    <v-container class="sub-container">
                        <v-row>
                            <v-col style="padding: 0;">
                                <v-col class="element">
                                    Convenient
                                    <v-img :src="require('../assets/LinkedConvenient.svg')" contain/>
                                </v-col>

                                <v-col class="element">
                                    Aligned
                                    <v-img :src="require('../assets/LinkedAligned.svg')" contain/>
                                </v-col>

                            </v-col>

                            <v-col class="element">
                                Ordered
                                <v-img :src="require('../assets/LinkedOrdered.svg')" contain/>
                            </v-col>
                        </v-row>
                    </v-container>
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
                        <v-col class="element">
                            Color (Luminance)
                            <v-img :src="require('../assets/Color(Luminance).svg')" contain/>
                        </v-col>

                        <v-col class="element">
                            Color (Hue)
                            <v-img :src="require('../assets/Color(Hue).svg')" contain/>
                        </v-col>
                    </v-row>

                    <v-row>
                        <v-col class="element">
                            3D Length
                            <v-img :src="require('../assets/3DLength.svg')" contain/>
                        </v-col>

                        <v-col class="element">
                            Glyph
                            <v-img :src="require('../assets/Glyph.svg')" contain/>
                        </v-col>
                    </v-row>

                    <v-row>
                        <v-col class="element">
                            Link (Line)
                            <v-img :src="require('../assets/Link(Line).svg')" contain/>
                        </v-col>

                        <v-col class="element">
                            Link (Arrow)
                            <v-img :src="require('../assets/Link(Arrow).svg')" contain/>
                        </v-col>
                    </v-row>

                    <v-row>
                        <v-col class="element">
                            Size
                            <v-img :src="require('../assets/Size.svg')" contain/>
                        </v-col>

                        <v-col class="element">
                            Quantity
                            <v-img :src="require('../assets/Quantity.svg')" contain/>
                        </v-col>
                    </v-row>
                </v-container>
            </v-expansion-panel-text>
        </v-expansion-panel>
    </v-expansion-panels>
</template>

<script>
export default {
    name: 'VisualSelector',

    props: {
        // functionToCall: {
        //     type: Function,
        //     required: true
        // }
    },

    methods: {

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

    .element{
        background-color: white;
    }

    .element:hover{
        transform: scale(1.2);
        border: 1px solid;
        border-color: #E1CBD8;
    }
</style>