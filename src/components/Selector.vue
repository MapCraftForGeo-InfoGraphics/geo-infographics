<template>
    <v-expansion-panels>
        <v-expansion-panel>

            <v-expansion-panel-title>
                Basic Map Representations
            </v-expansion-panel-title>
            <v-expansion-panel-text>
                <v-row>
                    <v-col>
                        <div class="element" id="Political-Map">
                            Political Map
                            <v-img :src="require('../assets/PoliticalMap.svg')" />
                        </div>

                        <div class="element" id="Shape-based-Map">
                            Shape-based Map
                            <v-img :src="require('../assets/Shape-basedMap.svg')" />
                        </div>

                        <div class="element" id="Grid-Cartogram">
                            Grid Cartogram
                            <v-img :src="require('../assets/GridCartogram.svg')" />
                        </div>
                    </v-col>

                    <v-col>
                        <div class="element" id="Topographic-Map">
                            Topographic Map
                            <v-img :src="require('../assets/TopographicMap.svg')" />
                        </div>

                        <div class="element" id="Street-Map">
                            Street Map
                            <v-img :src="require('../assets/StreetMap.svg')" />
                        </div>
                    </v-col>
                </v-row>
            </v-expansion-panel-text>
        </v-expansion-panel>


        <v-expansion-panel>
            <v-expansion-panel-title>
                Map Projections
            </v-expansion-panel-title>
            <v-expansion-panel-text>
                <v-row>
                    <v-col>
                        <div class="element" id="Mollweide">
                            Mollweide
                            <v-img :src="require('../assets/Mollweide.svg')" />
                        </div>
                    </v-col>

                    <v-col>
                        <div class="element" id="Robinson">
                            Robinson
                            <v-img :src="require('../assets/Robinson.svg')" />
                        </div>
                    </v-col>
                </v-row>
            </v-expansion-panel-text>
        </v-expansion-panel>


        <v-expansion-panel>
            <v-expansion-panel-title>
                Hightlight Techniques
            </v-expansion-panel-title>
            <v-expansion-panel-text>
                <v-row>
                    <v-col>
                        <div class="element" id="Light">
                            Light
                            <v-img :src="require('../assets/HighlightLight.svg')" />
                        </div>

                        <div class="element" id="Map-Pin">
                            Color
                            <v-img :src="require('../assets/HighlightMappin.svg')" />
                        </div>
                    </v-col>

                    <v-col>
                        <div class="element" id="Color">
                            Robinson
                            <v-img :src="require('../assets/HighlightColor.svg')" />
                        </div>

                        <div class="element" id="3D-Transformation">
                            Mollweide
                            <v-img :src="require('../assets/Highlight3d.svg')" />
                        </div>
                    </v-col>
                </v-row>

                <div class="element" id="Enlarged-Portions">
                    Mollweide
                    <v-img :src="require('../assets/HighlightEnlarge.svg')" width="60%"/>
                </div>
            </v-expansion-panel-text>
        </v-expansion-panel>



        <v-expansion-panel>
            <v-expansion-panel-title>
                Label Positions
            </v-expansion-panel-title>
            <v-expansion-panel-text>
                Some content 4
            </v-expansion-panel-text>
        </v-expansion-panel>


        <v-expansion-panel>
            <v-expansion-panel-title>
                Encoding Channels
            </v-expansion-panel-title>
            <v-expansion-panel-text>
                Some content 5
            </v-expansion-panel-text>
        </v-expansion-panel>

    </v-expansion-panels>
</template>

<script>
export default {
    name: 'ChannelSelector',

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