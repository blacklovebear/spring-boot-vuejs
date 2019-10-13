<template>
  
    <ProjectTable :project_info = "project_info" :jobInfo_list = "jobInfo_list" :jobInfo_items_list="jobInfo_items_list"/>
    
</template>
<script>
    import ProjectTable from "./ProjectTable";

    export default {
        components:{
            ProjectTable
        },

        
        data() {
            return {

                project_info: {
                    project_name: "珠海中海金鼎星筑苑",
                    contract_amount: 400.1
                },

                jobInfo_list : [
                            {id:1, title:"总监", price:1.01},
                            {id:2, title:"土建工程师", price: 2.01},
                            {id:3, title:"机电工程师", price: 3.01},
                            {id:4, title:"测量工程师", price: 4.01},
                            {id:5, title:"园林工程师", price: 5.01},
                            {id:6, title:"资料员", price:  6.01},
                        ],

                jobInfo_items_list: [
                    {
                        billing: 2,
                        cost:3,
                        month: "2019年7月",
                        details: [
                            {plan_c:1, real_c:2,},
                            {plan_c:1, real_c:2,},
                            {plan_c:1, real_c:2,},
                            {plan_c:1, real_c:2,},
                            {plan_c:1, real_c:2,},
                            {plan_c:1, real_c:2,},
                        ]
                    },

                    {
                        billing: 4,
                        cost:5,
                        month: "2019年8月",
                        details: [
                            {plan_c:2,  real_c:1,},
                            {plan_c:2,  real_c:1,},
                            {plan_c:2,  real_c:1,},
                            {plan_c:2,  real_c:1,},
                            {plan_c:2,  real_c:1,},
                            {plan_c:2,  real_c:1,},
                        ]
                    },

                    {
                        billing:7,
                        cost:85,
                        month: "2019年9月",
                        details: [
                            {plan_c:3,  real_c:4,},
                            {plan_c:3,  real_c:4,},
                            {plan_c:3,  real_c:4,},
                            {plan_c:3,  real_c:4,},
                            {plan_c:3,  real_c:4,},
                            {plan_c:3,  real_c:4,},
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
