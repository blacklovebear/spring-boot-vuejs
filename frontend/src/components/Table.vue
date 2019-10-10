<template>
    <div>

        <div class="col-md-3">
            <b-table striped hover :items="items"></b-table>
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
                    <!-- <b-tr>
                        <b-td>1</b-td> 
                        <b-td>总监理工程师</b-td> 
                        <b-td>2.82</b-td> 
                        <b-td>1</b-td> 
                        <b-td>2.82</b-td> 
                        <b-td>1</b-td> 
                        <b-td>2.82</b-td> 
                        <b-td>0</b-td> 
                        <b-td>-</b-td> 
                        <b-td style="vertical-align: middle" rowspan="6">-</b-td> 
                        <b-td style="vertical-align: middle" rowspan="6">-</b-td> 
                        <b-td style="vertical-align: middle" rowspan="6">-</b-td> 
                    </b-tr> -->

                    <b-tr  v-for="item in detail_items" :key='item.id' >
                        <b-td>{{item.id}}</b-td> 
                        <b-td>{{item.title}}</b-td> 
                        <b-td>{{item.price}}</b-td> 
                        <b-td>{{item.plan_c}}</b-td> 
                        <b-td>{{item.plan_n}}</b-td> 
                        <b-td>{{item.real_c}}</b-td> 
                        <b-td>{{item.real_n}}</b-td> 
                        <b-td>{{item.diff_c}}</b-td> 
                        <b-td>{{item.diff_n}}</b-td> 
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
                items: [
                    {name: '项目名称', value:    "珠海中海金鼎星筑苑"},
                    {name: '合约额', value:  262.10},
                    {name: '自开工累计应取费', value:     9.26},
                    {name: '自开工累计已取费', value:     9.72},
                    {name: '自开工累计未取费', value:     0.46},
                    {name: '自开工累计开票', value:  "-"},
                    {name: '自开工累计成本', value:  2.40},
                    {name: '结余', value:   -2.40},
                ],

                detail_items: [
                    {id:1, title:"总监", price:   2.82, plan_c:   1, plan_n:    2.82 ,        real_c: 0, real_n:    "-", diff_c:      -1, diff_n:   -2.82 },
                    {id:2, title:"土建工程师", price:    1.36, plan_c:   1, plan_n:    1.36 ,  real_c: 0, real_n:    "-", diff_c:      -1, diff_n:   -1.36 },
                    {id:3, title:"机电工程师", price:    1.58, plan_c:   0, plan_n:    "-" ,     real_c: 0, real_n:    "-", diff_c:      0, diff_n:    "-"   },
                    {id:4, title:"测量工程师", price:    1.02, plan_c:   1, plan_n:    1.02,   real_c:0, real_n:    "-", diff_c:      -1, diff_n:   -1.02 },
                    {id:5, title:"园林工程师", price:    1.02, plan_c:   0, plan_n:    "-"  ,    real_c:0, real_n:    "-", diff_c:      0, diff_n:    "-"   },
                    {id:6, title:"资料员", price:  0.90, plan_c:   1, plan_n:    0.90 ,       real_c: 0, real_n:    "-", diff_c:      -1, diff_n:   -0.90 },
                ]
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
