<template>
    <div class="viewer">
        <vc-viewer ref="viewer" @ready="ready" @LEFT_CLICK="onClick">

            <vc-primitive ref="primitive" :appearance="appearance">
                <vc-instance-geometry id="0" :attributes="attributes1">
                    <vc-geometry-polygon
                        ref="polygon1"
                        :polygon-hierarchy="polygon1Hierarchy"
                        :height="height"
                    ></vc-geometry-polygon>
                </vc-instance-geometry>
                <vc-instance-geometry id="1" :attributes="attributes2">
                    <vc-geometry-polygon
                        ref="polygon2"
                        :polygon-hierarchy="polygon2Hierarchy"
                        :height="height"
                    ></vc-geometry-polygon>
                </vc-instance-geometry>
            </vc-primitive>
        </vc-viewer>
    </div>
</template>

<script>
export default {
    name: 'TestCesium',
    data() {
        return {
            appearance: null,
            geometry: null,
            vertexFormat: null,
            polygon1Hierarchy: [
                { lng: 102.1, lat: 29.5 },
                { lng: 106.2, lat: 29.5 },
                { lng: 106.2, lat: 35.5 },
                { lng: 100.1, lat: 35.5 }
            ],
            polygon2Hierarchy: [
                { lng: 107.1, lat: 29.5 },
                { lng: 110.2, lat: 29.5 },
                { lng: 110.2, lat: 35.5 },
                { lng: 107.1, lat: 35.5 }
            ],
            height: 100,
            attributes1: null,
            attributes2: null
        }
    },
    mounted() {
        // Promise.all([
        //     this.$refs.polygon.createPromise
        //     // this.$refs.polygonOutline.createPromise
        // ]).then((instances) => {
        //     // const Cesium = instances.Cesium
        //     console.log('All geometries are loaded.')
        //     // instances[0].viewer.zoomTo(instances[0].viewer.entities)
        //     // const boundingSphereUnion = instances.reduce((prev, cur) => {
        //     //     const geometry = cur.cesiumObject.constructor.createGeometry(
        //     //         cur.cesiumObject
        //     //     )
        //     //     const boundingSphere = cur.vm.$parent.modelMatrix
        //     //         ? Cesium.BoundingSphere.transform(
        //     //               geometry.boundingSphere,
        //     //               cur.vm.$parent.modelMatrix
        //     //           )
        //     //         : geometry.boundingSphere
        //     //     return prev === null
        //     //         ? boundingSphere
        //     //         : Cesium.BoundingSphere.union(prev, boundingSphere)
        //     // }, null)
        //     // instances[0].viewer.scene.camera.flyToBoundingSphere(
        //     //     boundingSphereUnion
        //     // )
        // })
    },
    methods: {
        ready({ Cesium, viewer }) {
            this.Cesium = Cesium
            this.viewer = viewer
            const {
                PerInstanceColorAppearance,
                ColorGeometryInstanceAttribute
                // EllipsoidSurfaceAppearance
                // Material
            } = Cesium
            this.attributes1 = {
                color: new ColorGeometryInstanceAttribute(
                    Math.random(),
                    Math.random(),
                    Math.random(),
                    1
                )
            }
            this.attributes2 = {
                color: new ColorGeometryInstanceAttribute(
                    Math.random(),
                    Math.random(),
                    Math.random(),
                    1
                )
            }
            this.appearance = new PerInstanceColorAppearance({
                flat: true
            })
        },
        onClick(click) {
            const viewer = this.$refs.viewer
            const Cesium = this.$refs.viewer.Cesium
            const primitive = this.$refs.primitive.cesiumObject
            const pickedObject = this.viewer.scene.pick(click.position)
            if (pickedObject) {
                // console.log(pickedObject)
                // console.log(primitive)

                const attributes = primitive.getGeometryInstanceAttributes(
                    pickedObject.id
                )
                attributes.color = Cesium.ColorGeometryInstanceAttribute.toValue(
                    Cesium.Color.fromRandom({ alpha: 1.0 })
                )
                // console.log(this.$refs.viewer)
                // const entityId = pickedObject.id._id
                // this.selectCommunity(entityId)
                this.Cesium.SelectionIndicator('0', viewer.scene)
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
