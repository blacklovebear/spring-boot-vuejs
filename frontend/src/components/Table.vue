<template>
    <div>

        <div class="row">
                <div class="col-md-3">
                    <b-table striped hover :items="project_info_computed" thead-class="hidden_header"></b-table>
                </div>

                <div class="col-md-9">
                    <div class="form-group" v-for="jobInfo in jobInfo_list">
                        <div class="row">
                            <label class="col-md-2" :for="jobInfo.title">{{jobInfo.title}}</label>
                            <input type="text" class="col-md-2 form-control" :id="jobInfo.title" v-model="jobInfo.price">
                        </div>
                            
                    </div>
                </div>

        </div>

        <div v-for="items in items_list" class="col-md-6">
            <DetailTable :items = "items" :jobInfo_list = "jobInfo_list"/>
        </div>
    </div>
</template>
<script>
    import DetailTable from "./DetailTable";

    export default {
        components:{
            DetailTable
        },

        computed: {
             items_total_computed: function () {
                var total_plan_n = 0
                var total_reel_n = 0

                var total_billing = 0
                var total_cost = 0

                for (let [i, item] of this.items_list.entries()) {
                    for (let [k, detail] of item.details.entries()) {
                        total_plan_n += this.jobInfo_list[k].price * detail.plan_c;
                        total_reel_n += this.jobInfo_list[k].price * detail.real_c;

                    }
                    total_billing += item.billing
                    total_cost += item.cost
                }

                let total_diff_n = total_reel_n - total_plan_n
                let total_balance = total_billing - total_cost

                return {
                    total_plan_n: total_plan_n,
                    total_reel_n: total_reel_n,
                    total_diff_n: total_diff_n,
                    total_billing: total_billing,
                    total_cost: total_cost,
                    total_balance: total_balance
                }
            },

            project_info_computed : function () {
                return [
                    {name: '项目名称', value:    "珠海中海金鼎星筑苑"},
                    {name: '合约额', value:  262.10},
                    {name: '自开工累计应取费', value: this.items_total_computed.total_plan_n },
                    {name: '自开工累计已取费', value: this.items_total_computed.total_reel_n },
                    {name: '自开工累计未取费', value: this.items_total_computed.total_diff_n },
                    {name: '自开工累计开票', value: this.items_total_computed.total_billing },
                    {name: '自开工累计成本', value: this.items_total_computed.total_cost },
                    {name: '结余', value: this.items_total_computed.total_balance }
                ]
            
            }
        },

        data() {
            return {
                jobInfo_list : [
                            {id:1, title:"总监", price:2.82},
                            {id:2, title:"土建工程师", price: 1.36},
                            {id:3, title:"机电工程师", price: 1.58},
                            {id:4, title:"测量工程师", price: 1.02},
                            {id:5, title:"园林工程师", price: 1.02},
                            {id:6, title:"资料员", price:  0.90},
                        ],

                items_list: [
                    {
                        billing: 2,
                        cost:3,
                        details: [
                            {plan_c:1, real_c: 0,},
                            {plan_c:1, real_c: 0,},
                            {plan_c:0, real_c: 1,},
                            {plan_c:1, real_c:0,},
                            {plan_c:0, real_c:0,},
                            {plan_c:1, real_c: 0,},
                        ]
                    },

                    {
                        billing: 4,
                        cost:5,
                        details: [
                            {plan_c:1,  real_c: 0,},
                            {plan_c:1,  real_c: 1,},
                            {plan_c:0,  real_c: 0,},
                            {plan_c:3,  real_c:0,},
                            {plan_c:4,  real_c:0,},
                            {plan_c:5,  real_c: 0,},
                        ]
                    },

                    {
                        billing:7,
                        cost:85,
                        details: [
                            {plan_c:1,  real_c: 0,},
                            {plan_c:1,  real_c: 1,},
                            {plan_c:0,  real_c: 0,},
                            {plan_c:3,  real_c:0,},
                            {plan_c:4,  real_c:0,},
                            {plan_c:5,  real_c: 0,},
                        ]
                    },
                ],
            }
        },

    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.col-md-6 {
    display: inline-block;
}

.form-group label {
    text-align: right
}

</style>


<style>
.hidden_header {
  display: none;
}
</style>
