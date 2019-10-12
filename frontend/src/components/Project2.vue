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
                    project_name: "广州中海亚运大道北地块",
                    contract_amount: 500.02
                },

                jobInfo_list : [
                            {id:1, title:"总监", price:6.02},
                            {id:2, title:"土建工程师", price: 5.02},
                            {id:3, title:"机电工程师", price: 4.02},
                            {id:4, title:"测量工程师", price: 3.02},
                            {id:5, title:"园林工程师", price: 2.02},
                            {id:6, title:"资料员", price:  1.02},
                        ],

                jobInfo_items_list: [
                    {
                        billing: 2,
                        cost:3,
                        details: [
                            {plan_c:4, real_c:5,},
                            {plan_c:4, real_c:5,},
                            {plan_c:4, real_c:5,},
                            {plan_c:4, real_c:5,},
                            {plan_c:4, real_c:5,},
                            {plan_c:4, real_c:5,},
                        ]
                    },

                    {
                        billing: 4,
                        cost:5,
                        details: [
                            {plan_c:3,  real_c:2,},
                            {plan_c:3,  real_c:2,},
                            {plan_c:3,  real_c:2,},
                            {plan_c:3,  real_c:2,},
                            {plan_c:3,  real_c:2,},
                            {plan_c:3,  real_c:2,},
                        ]
                    },

                    {
                        billing:7,
                        cost:85,
                        details: [
                            {plan_c:1,  real_c:1,},
                            {plan_c:1,  real_c:1,},
                            {plan_c:1,  real_c:1,},
                            {plan_c:1,  real_c:1,},
                            {plan_c:1,  real_c:1,},
                            {plan_c:1,  real_c:1,},
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
