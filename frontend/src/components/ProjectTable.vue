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
                            <input type="text" class="col-md-2 form-control" :id="jobInfo.title" v-model.number="jobInfo.price">
                        </div>
                            
                    </div>
                </div>

        </div>

        <div v-for="items in jobInfo_items_list" class="col-md-6">
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

        props: ["jobInfo_list", "project_info", "jobInfo_items_list"],

        computed: {
             items_total_computed: function () {
                var total_plan_n = 0
                var total_reel_n = 0

                var total_billing = 0
                var total_cost = 0

                for (let [i, item] of this.jobInfo_items_list.entries()) {
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
                    {name: '项目名称', value: this.project_info.project_name},
                    {name: '合约额', value:  this.project_info.contract_amount},
                    {name: '自开工累计应取费', value: this.items_total_computed.total_plan_n.toFixed(2)},
                    {name: '自开工累计已取费', value: this.items_total_computed.total_reel_n.toFixed(2)},
                    {name: '自开工累计未取费', value: this.items_total_computed.total_diff_n.toFixed(2)},
                    {name: '自开工累计开票', value: this.items_total_computed.total_billing.toFixed(2)},
                    {name: '自开工累计成本', value: this.items_total_computed.total_cost.toFixed(2)},
                    {name: '结余', value: this.items_total_computed.total_balance.toFixed(2)}
                ]
            
            }
        },

        data() {
            return {

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
