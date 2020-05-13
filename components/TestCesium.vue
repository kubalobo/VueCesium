<template>
    <div class="viewer">
        <vc-viewer
            ref="viewer"
            @ready="ready"
            @selectedEntityChanged="selectedEntityChanged"
        >
            <vc-entity
                v-for="polygon in this.polygons"
                :id="polygon.id"
                :key="polygon.id"
                :description="polygon.name"
            >
                <vc-graphics-polygon
                    :hierarchy="polygon.hierarchy"
                    :material="polygon.material"
                ></vc-graphics-polygon>
            </vc-entity>
        </vc-viewer>
    </div>
</template>

<script>
export default {
    name: 'TestCesium',
    props: { polygons: Array, selected: String },
    data() {
        return {
            // entities: []
        }
    },
    watch: {
        selected(val) {
            console.log('Cesium watcher')
            if (this.viewer)
                this.viewer.selectedEntity = this.viewer.entities.values[val]
        }
    },
    methods: {
        ready({ Cesium, viewer }) {
            this.Cesium = Cesium
            this.viewer = viewer
            // viewer.zoomTo(viewer.entities) // or in mounted method after ref promise... ???? TODO
        },
        selectedEntityChanged(entity) {
            if (entity) {
                entity.polygon.material = this.Cesium.Color.fromRandom({
                    minimumAlpha: 0.8
                })
                this.$emit('polygonChanged', entity.id)
            }
        }
    }
}
</script>

<style scoped>
.viewer {
    width: 100%;
    height: 400px;
}
</style>
