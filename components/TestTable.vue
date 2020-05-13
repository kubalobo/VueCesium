<template>
    <el-table
        ref="tableee"
        :data="this.polygons"
        style="width: 100%"
        highlight-current-row
        @current-change="handleCurrentChange"
    >
        <el-table-column> </el-table-column>
        <el-table-column prop="id" label="ID" width="80"> </el-table-column>
        <el-table-column prop="name" label="Name" width="300">
        </el-table-column>
    </el-table>
</template>

<script>
export default {
    name: 'TestTable',
    props: {
        polygons: Array,
        selected: String
    },
    data() {
        return {
            currentRow: null
        }
    },
    watch: {
        selected(val) {
            console.log('Table watcher: ' + val)
            if (this.currentRow.id !== val) {
                this.setCurrent(this.polygons[val])
            }
        }
    },
    mounted() {
        this.setCurrent(this.selected)
    },
    methods: {
        handleCurrentChange(currentRow, oldCurrentRow) {
            this.currentRow = currentRow
            if (currentRow.id) this.$emit('polygonChanged', currentRow.id)
        },
        setCurrent(row) {
            this.$refs.tableee.setCurrentRow(row)
        }
    }
}
</script>

<style scoped></style>
