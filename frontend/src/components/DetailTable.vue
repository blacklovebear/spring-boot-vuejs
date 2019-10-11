<template>
    <b-table-simple hover small caption-top responsive>
        <b-thead head-variant="light">
            <b-tr >
                <b-th style="vertical-align: middle" rowspan="3">序号</b-th>
                <b-th style="vertical-align: middle" rowspan="3">岗位名称</b-th>
                <b-th style="vertical-align: middle" rowspan="3">人月综合单价</b-th>
                <b-th colspan="12">2019年7月</b-th>
            </b-tr>
            <b-tr>
                <b-th coloffset="3" colspan="2">计划</b-th>
                <b-th colspan="2">实际</b-th>
                <b-th colspan="2">差异</b-th>
                <b-th  style="vertical-align: middle" rowspan="2">开票</b-th>
                <b-th  style="vertical-align: middle" rowspan="2">成本</b-th>
                <b-th  style="vertical-align: middle" rowspan="2">结余</b-th>
            </b-tr>
            <b-tr>
                <b-th coloffset="3">人数</b-th>
                <b-th >取费</b-th>
                <b-th >人数</b-th>
                <b-th >取费</b-th>
                <b-th >人数</b-th>
                <b-th >人月综合单价</b-th>
            </b-tr>
        </b-thead>
        <b-tbody>

            <b-tr v-for="(item, index) in items_computed" :key='item.id' >
                <b-td>{{jobInfo_list[index].id}}</b-td>
                <b-td>{{jobInfo_list[index].title}}</b-td>
                <b-td>{{jobInfo_list[index].price}}</b-td>

                <b-td>{{item.plan_c}}</b-td>
                <b-td>{{item.plan_n}}</b-td>
                <b-td>{{item.real_c}}</b-td>
                <b-td>{{item.real_n}}</b-td>
                <b-td>{{item.diff_c}}</b-td>
                <b-td>{{item.diff_n}}</b-td>

                <!-- 还不清楚计算逻辑 -->
                <b-td v-if="index == 0" style="vertical-align: middle" :rowspan="items_computed.length + 1">{{items.billing}}</b-td>
                <b-td v-if="index == 0" style="vertical-align: middle" :rowspan="items_computed.length + 1">{{items.cost}}</b-td>
                <b-td v-if="index == 0" style="vertical-align: middle" :rowspan="items_computed.length + 1">{{items.billing - items.cost}}</b-td>
            </b-tr>


            <b-tr >
                <b-td colspan="3">合计</b-td>

                <b-td>{{items_computed_sum.plan_c_sum}}</b-td>
                <b-td>{{items_computed_sum.plan_n_sum}}</b-td>
                <b-td>{{items_computed_sum.real_c_sum}}</b-td>
                <b-td>{{items_computed_sum.real_n_sum}}</b-td>
                <b-td>{{items_computed_sum.diff_c_sum}}</b-td>
                <b-td>{{items_computed_sum.diff_n_sum}}</b-td>
            </b-tr>



        </b-tbody>
    </b-table-simple>

</template>

<script>
    export default {
        name: 'detailTable',

        data() {
            return {
            }
        },

        props: ["items", "jobInfo_list"],

        computed: {
            items_computed: function () {
                let result = []

                for (let [i, item] of this.items.details.entries()) {
                    item.plan_n = this.jobInfo_list[i].price * item.plan_c;
                    item.real_n = this.jobInfo_list[i].price * item.real_c;

                    item.diff_c = item.real_c - item.plan_c;
                    item.diff_n = item.real_n - item.plan_n;
                    result.push(item);
                }

                return result
            },


            // a computed getter
            items_computed_sum: function () {
                // `this` points to the vm instance
                let plan_c_sum = this.items_computed.map(item => item.plan_c).reduce((acc, plan_c) => acc + plan_c, 0)
                let plan_n_sum = this.items_computed.map(item => item.plan_n).reduce((acc, plan_n) => acc + plan_n, 0)
                let real_c_sum = this.items_computed.map(item => item.real_c).reduce((acc, real_c) => acc + real_c, 0)
                let real_n_sum = this.items_computed.map(item => item.real_n).reduce((acc, real_n) => acc + real_n, 0)
                let diff_c_sum = this.items_computed.map(item => item.diff_c).reduce((acc, diff_c) => acc + diff_c, 0)
                let diff_n_sum = this.items_computed.map(item => item.diff_n).reduce((acc, diff_n) => acc + diff_n, 0)
                return {
                    plan_c_sum: plan_c_sum,
                    plan_n_sum: plan_n_sum,
                    real_c_sum: real_c_sum,
                    real_n_sum: real_n_sum,
                    diff_c_sum: diff_c_sum,
                    diff_n_sum: diff_n_sum
                }
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
