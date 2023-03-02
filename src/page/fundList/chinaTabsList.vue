<template>
    <div class="fillcontain">
        <div class="tabContainer" ref="tabContainer">
            <el-tabs type="border-card" >
                <el-tab-pane>
                    <span slot="label" @click="toggleTabs('eastChina')"><icon-svg icon-class="icondashboard" />华东区域</span>
                </el-tab-pane>
                <el-tab-pane>
                    <span slot="label" @click="toggleTabs('southChina')"><icon-svg icon-class="iconecharts" />华南区域</span>
                    <!-- <china-tabs-table :toggleData="toggleData"></china-tabs-table> -->
                </el-tab-pane>
                <el-tab-pane>
                    <span slot="label" @click="toggleTabs('centralChina')"><icon-svg icon-class="iconinfo" />华中区域</span>
                    <!-- <china-tabs-table :toggleData="toggleData"></china-tabs-table> -->
                </el-tab-pane>
                <el-tab-pane>
                    <span slot="label" @click="toggleTabs('northChina')"><icon-svg icon-class="iconpermission" />华北区域</span>
                <!-- <china-tabs-table :toggleData="toggleData"></china-tabs-table> -->
                </el-tab-pane>
                <el-tab-pane>
                    <span slot="label" @click="toggleTabs('northwestChina')"><icon-svg icon-class="iconuser" />西北区域</span>
                    <!-- <china-tabs-table :toggleData="toggleData"></china-tabs-table> -->
                </el-tab-pane>
                <el-tab-pane>
                    <span slot="label" @click="toggleTabs('southwestChina')"><icon-svg icon-class="iconError" />西南地区</span>
                    <!-- <china-tabs-table :toggleData="toggleData"></china-tabs-table> -->
                </el-tab-pane>
                <el-tab-pane>
                     <span slot="label" @click="toggleTabs('northeastChina')"><icon-svg icon-class="iconfufei0" />东北地区</span>
                     <!-- <china-tabs-table :toggleData="toggleData"></china-tabs-table> -->
                </el-tab-pane>
                <el-tab-pane>
                     <span slot="label" @click="toggleTabs('specialareaChina')"><icon-svg icon-class="iconpay1" />台港澳地区</span>
                     <!-- <china-tabs-table :toggleData="toggleData"></china-tabs-table> -->
                </el-tab-pane>
                <keep-alive>
                    <china-tabs-table :limit="incomePayData.limit" :page=incomePayData.page  :toggleData="toggleData" @PAGE_LEN="getPage"></china-tabs-table>
                </keep-alive>
            </el-tabs>
            <!-- <pagination :pageTotal="pageTotal" @PAGE_LEN="getPage()"></pagination> -->
            <pagination :page="incomePayData.page" :limit="incomePayData.limit" :pageTotal="pageTotal" @handleCurrentChange="handleCurrentChange" @handleSizeChange="handleSizeChange"></pagination>

        </div>
    </div>
</template>

<script>
    import chinaTabsTable from './components/chinaTabsTable'
    import data from './data/chinaTabs.json';
    import Pagination from "@/components/pagination";

export default {
    data() {
        return {
            toggleData: '',
            pageTotal: 60,
            incomePayData:{
                    page:1,
                    limit:10,
                    name:''
                },
        }
    },
    components: {
        chinaTabsTable,
        Pagination
    },
    mounted() {
        //  this.setTabHeight();
        //  window.onresize = () => {
        //     this.setTabHeight();
        //  }
        this.toggleTabs('eastChina');
        // console.log(this.toggleData);
    },
    methods: {
        setTabHeight() {
            this.$nextTick(() => {
                this.$refs.tabContainer.style.height = (document.body.clientHeight - 160) + 'px'
            })
        },
        toggleTabs(item) {
            this.toggleData = item;
            this.incomePayData = {
                page: 1,
                limit: 10,
                name: ''
            };
        },
        getPage(length) {
            // console.log('1321312312312312');\
            this.pageTotal=length
            // console.log(length);
        },
        handleCurrentChange(val) {
            this.incomePayData.page = val;
            // this.getMoneyList()
        },
        // 每页显示多少条
        handleSizeChange(val) {
            this.incomePayData.limit = val;
            // this.getMoneyList()
        }
    }
}
</script>

<style lang="less" scoped>
 
</style>


