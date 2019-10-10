<template>
    <div>

        <div class="col-md-3">
            <b-table striped hover :items="items_total"></b-table>
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
                        detail: [
                            {plan_c:1,real_c: 0,},
                            {plan_c:1, real_c: 0,},
                            {plan_c:0,  real_c: 0,},
                            {plan_c:1,  real_c:0,},
                            {plan_c:0,  real_c:0,},
                            {plan_c:1,  real_c: 0,},
                        ]
                    },

                    {
                        billing: 4,
                        cost:5,
                        detail: [
                            {plan_c:1,real_c: 0,},
                            {plan_c:1, real_c: 0,},
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

</style>
