<template>
    <div>

        <div class="col-md-3">
            <b-table striped hover :items="items_total"></b-table>
        </div>

        <div class="col-md-6">
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
    
                    <b-tr  v-for="(item, index) in items_computed" :key='item.id' >
                        <b-td>{{item.id}}</b-td>
                        <b-td>{{item.title}}</b-td>
                        <b-td>{{item.price}}</b-td>

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
        </div>


    </div>

</template>

<script>
    export default {
        data() {
            return {
                items_total: [
                    {name: '项目名称', value:    "珠海中海金鼎星筑苑"},
                    {name: '合约额', value:  262.10},
                    {name: '自开工累计应取费', value:     9.26},
                    {name: '自开工累计已取费', value:     9.72},
                    {name: '自开工累计未取费', value:     0.46},
                    {name: '自开工累计开票', value:  0},
                    {name: '自开工累计成本', value:  2.40},
                    {name: '结余', value:   -2.40},
                ],

                items: {
                    billing: 2,
                    cost:3,
                    detail: [
                        {id:1, title:"总监", price:2.82, plan_c:1,real_c: 0,},
                        {id:2, title:"土建工程师", price: 1.36, plan_c:1, real_c: 0,},
                        {id:3, title:"机电工程师", price: 1.58, plan_c:0,  real_c: 0,},
                        {id:4, title:"测量工程师", price: 1.02, plan_c:1,  real_c:0,},
                        {id:5, title:"园林工程师", price: 1.02, plan_c:0,  real_c:0,},
                        {id:6, title:"资料员", price:  0.90, plan_c:1,  real_c: 0,},
                    ]
                },
            }
        },

        computed: {
            items_computed: function () {
                return this.items.detail.map(item =>  {
                    item.plan_n = item.price * item.plan_c;
                    item.real_n = item.price * item.real_c;

                    item.diff_c = item.real_c - item.plan_c;
                    item.diff_n = item.real_n - item.plan_n;
                    return item;
                });
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
