<template>
    <div class="chinaTabsTable">
        <el-table :data="tableData" style="width: 100%" align='center'>
            <el-table-column prop="ID" label="序号" align='center' width="80">
                <template slot-scope="scope">
                    {{ scope.$index + 1 }}
                </template>
            </el-table-column>
            <el-table-column prop="provinces" label="省份" align='center' width="140">
            </el-table-column>
            <el-table-column prop="orderMoney" label="投资总额" align='center' width="120" sortable>
                <template slot-scope="scope">
                    <span style="color:#CC0033">{{ scope.row.orderMoney }}</span>
                </template>
            </el-table-column>
            <el-table-column prop="incomeMoney" label="收益金额" align='center' width="120" sortable>
                <template slot-scope="scope">
                    <span style="color:#00d053;">+{{ scope.row.incomeMoney }}</span>
                </template>
            </el-table-column>
            <el-table-column prop="payType" label="主要投资项目" align='center' width="120">
                <template slot-scope="scope">
                    <el-tag type="info" close-transition>
                        {{ scope.row.payType }}
                    </el-tag>
                </template>
            </el-table-column>
            <el-table-column prop="orderPeriod" label="投资周期" align='center' width="120">
            </el-table-column>
            <el-table-column prop="orderPersonConunt" label="投资人数" align='center' width="120">
            </el-table-column>
            <el-table-column prop="orderYearRate" label="投资年变化率" align='center' width='120'>
            </el-table-column>
            <el-table-column prop="remarks" label="备注" align='left'>
                <template slot-scope="scope">
                    <span style="color:#3366CC">{{ scope.row.remarks }}</span>
                </template>
            </el-table-column>
        </el-table>
    </div>
</template>

<script>
import data from '../data/chinaTabs.json';

export default {
    data() {
        return {
            tableData: [],
            tableHeight: 0,
            incomePayData: {
                page: 1,
                limit: 10,
                name: ''
            },
        }
    },
    props: {
        toggleData: [String],
        limit: [Number],
        page: [Number]
    },
    mounted() {
        // this.init()
        this.setTableHeight();
        window.onresize = () => {
            this.setTableHeight();
        }
        //  console.log(this.tableData);

    },
    methods: {
        setTableHeight() {
            this.$nextTick(() => {
                this.tableHeight = document.body.clientHeight - 280
            })
        },
        showTableData(item) {
            switch (item) {
                case 'eastChina':
                    this.tableData = data.china.eastChina;
                    break;
                case 'southChina':
                    this.tableData = data.china.southChina;
                    break;
                case 'centralChina':
                    this.tableData = data.china.centralChina;
                    break;
                case 'northChina':
                    this.tableData = data.china.northChina;
                    break;
                case 'northwestChina':
                    this.tableData = data.china.northwestChina;
                    break;
                case 'southwestChina':
                    this.tableData = data.china.southwestChina;
                    break;
                case 'northeastChina':
                    this.tableData = data.china.northeastChina;
                    break;
                case 'specialareaChina':
                    this.tableData = data.china.specialareaChina;
                    break;
            }
            this.sendPage()
        },
        sendPage() {
            // console.log('send page_len');
            //  console.log(this.tableData.length);
            let table_len = this.tableData.length
            this.$emit('PAGE_LEN', table_len)
            // console.log(this.toggleData);
        },
        init() {
            // console.log(this.toggleData);
            this.showTableData(this.toggleData)
            // console.log(console.log(this.tableData));
            // console.log('init');
            this.change(this.incomePayData.limit, this.incomePayData.page)
            // console.log("end");
            // console.log(this.tableData);
            console.log('init');
        },
        change(limit, page) {
            this.showTableData(this.toggleData)
            this.tableData = this.tableData.slice((page - 1) * limit, (page - 1) * limit + limit)
            console.log('fdaasdfas');
             console.log(limit);
        }
    },
    watch: {
        // 监听属性的变化，可以接收参数;
        toggleData(v) {
            this.showTableData(v);
            // this.init()
            // console.log(this.toggleData);
            this.change(this.incomePayData.limit,this.incomePayData.page)
            console.log('watch');
        },
        limit(v) {
            console.log("new limit4353453454  " + v);
            this.change(this.limit, this.page)
        },
        page(v) {
            console.log("new page453534534534  " + v);
            this.change(this.limit, this.page)

        },

    }
}
</script>

<style lang="less"></style>
