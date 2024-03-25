<template>
    <v-expansion-panels>
        <v-expansion-panel>
            <v-expansion-panel-title>
                Basic Map Representations
            </v-expansion-panel-title>

            <v-expansion-panel-text>
                <v-container class="container">
                    <v-row>
                        <v-col>
                            Political Map
                            <v-img :src="require('../assets/PoliticalMap.svg')" />
                        </v-col>

                        <v-col>
                            Topographic Map
                            <v-img :src="require('../assets/TopographicMap.svg')" />
                        </v-col>
                    </v-row>

                    <v-row>
                        <v-col>
                            Shape-based Map
                            <v-img :src="require('../assets/Shape-basedMap.svg')" />
                        </v-col>

                        <v-col>
                            Street Map
                            <v-img :src="require('../assets/StreetMap.svg')" />
                        </v-col>
                    </v-row>

                    <v-row>
                        <v-col>
                            Grid Cartogram
                            <v-img :src="require('../assets/GridCartogram.svg')" />
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
                        <v-col>
                            Mollweide
                            <v-img :src="require('../assets/Mollweide.svg')" />
                        </v-col>

                        <v-col>
                            Robinson
                            <v-img :src="require('../assets/Robinson.svg')" />
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
                        <v-col>
                            Light
                            <v-img :src="require('../assets/HighlightLight.svg')" />
                        </v-col>

                        <v-col>
                            Robinson
                            <v-img :src="require('../assets/HighlightColor.svg')" />
                        </v-col>
                    </v-row>

                    <v-row>
                        <v-col>
                            Color
                            <v-img :src="require('../assets/HighlightMappin.svg')" />
                        </v-col>
                        <v-col>
                            Mollweide
                            <v-img :src="require('../assets/Highlight3d.svg')" />
                        </v-col>
                    </v-row>

                    <v-row>
                        <v-col>
                            Mollweide
                            <v-img :src="require('../assets/HighlightEnlarge.svg')" width="60%" />
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
                            <v-col>
                                Situated
                                <v-img :src="require('../assets/Situated.svg')" />
                            </v-col>

                            <v-col></v-col>
                        </v-row>
                    </v-container>

                    <div class="sub-title">Matched</div>
                    <v-container class="sub-container">
                        <v-row>
                            <v-col>
                                Text
                                <v-img :src="require('../assets/MatchedText.svg')" />
                            </v-col>

                            <v-col>
                                Icon
                                <v-img :src="require('../assets/MatchedIcon.svg')" />
                            </v-col>
                        </v-row>

                        <v-row>
                            <v-col>
                                Color
                                <v-img :src="require('../assets/MathchedColor.svg')" />
                            </v-col>
                            <v-col></v-col>
                        </v-row>
                    </v-container>

                    <div class="sub-title">Linked</div>
                    <v-container class="sub-container">
                        <v-row>
                            <v-col style="padding: 0;">
                                <v-col>
                                    Convenient
                                    <v-img :src="require('../assets/LinkedConvenient.svg')" />
                                </v-col>

                                <v-col>
                                    Aligned
                                    <v-img :src="require('../assets/LinkedAligned.svg')" />
                                </v-col>

                            </v-col>

                            <v-col>
                                Ordered
                                <v-img :src="require('../assets/LinkedOrdered.svg')" />
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
                        <v-col>
                            Color (Luminance)
                            <v-img :src="require('../assets/Color(Luminance).svg')" />
                        </v-col>

                        <v-col>
                            Color (Hue)
                            <v-img :src="require('../assets/Color(Hue).svg')" />
                        </v-col>
                    </v-row>

                    <v-row>
                        <v-col>
                            3D Length
                            <v-img :src="require('../assets/3DLength.svg')" />
                        </v-col>

                        <v-col>
                            Glyph
                            <v-img :src="require('../assets/Glyph.svg')" />
                        </v-col>
                    </v-row>

                    <v-row>
                        <v-col>
                            Link (Line)
                            <v-img :src="require('../assets/Link(Line).svg')" />
                        </v-col>

                        <v-col>
                            Link (Arrow)
                            <v-img :src="require('../assets/Link(Arrow).svg')" />
                        </v-col>
                    </v-row>

                    <v-row>
                        <v-col>
                            Size
                            <v-img :src="require('../assets/Size.svg')" />
                        </v-col>

                        <v-col>
                            Quantity
                            <v-img :src="require('../assets/Quantity.svg')" />
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

    components: {

    },

    data: () => ({

    }),

    mounted() {

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
</style>