<template>
    <div class="container">
        <div>
            <h1 class="title">
                Proof of concept <br />CESIUM zsynchronizowane z tabelą w
                oparciu o Vue.js
            </h1>
            <test-cesium
                :polygons="polygons"
                :selected="selectedPolygon"
                @polygonChanged="changePolygon"
            />
            <TestTable
                :polygons="polygons"
                :selected="selectedPolygon"
                @polygonChanged="changePolygon"
            />
        </div>
    </div>
</template>

<script>
import TestTable from '../components/TestTable'
import TestCesium from '../components/TestCesium'

export default {
    components: {
        TestCesium,
        TestTable
    },
    data() {
        return {
            polygons: [
                {
                    id: '0',
                    name: 'Pierwszy poligon',
                    hierarchy: [
                        { lng: 102.1, lat: 29.5 },
                        { lng: 106.2, lat: 29.5 },
                        { lng: 106.2, lat: 35.5 },
                        { lng: 100.1, lat: 35.5 }
                    ],
                    material: 'red'
                },
                {
                    id: '1',
                    name: 'Drugi poligon',
                    hierarchy: [
                        { lng: 108.1, lat: 29.5 },
                        { lng: 112.2, lat: 29.5 },
                        { lng: 112.2, lat: 35.5 },
                        { lng: 108.1, lat: 35.5 }
                    ],
                    material: 'blue'
                },
                {
                    id: '2',
                    name: 'Trzeci poligon',
                    hierarchy: [
                        { lng: 102.1, lat: 36.5 },
                        { lng: 112.2, lat: 36.5 },
                        { lng: 112.2, lat: 45.5 },
                        { lng: 102.1, lat: 45.5 }
                    ],
                    material: 'green'
                }
            ],
            selectedPolygon: '0'
        }
    },
    methods: {
        changePolygon(id) {
            this.selectedPolygon = id
        }
    }
}
</script>

<style>
.container {
    margin: 0 auto;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    width: 600px;
}
.title {
    font-family: 'Quicksand', 'Source Sans Pro', -apple-system,
        BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial,
        sans-serif;
    display: block;
    font-weight: 300;
    font-size: 30px;
    color: #35495e;
    letter-spacing: 1px;
    padding-bottom: 15px;
}
</style>
