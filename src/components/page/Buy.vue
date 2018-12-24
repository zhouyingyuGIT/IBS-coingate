<template>
    <div>
        <el-row :gutter="20">
            <el-col :span="6" v-for="item in items" :key="item.id">
                <el-card class="bank_transfer" shadow="hover" :body-style="{padding: '0px'}">
                    <div class="logo">
                        <img v-bind:src="item.imgURL" style="max-height: 64px;max-width: 200px;">
                    </div>
                    <div class="card-block">
                        <h4 class="card-title">{{ item.name }}</h4>
                        <div class="text-muted">
                            <b>{{ item.muted }}</b>
                        </div>
                        <hr style="width: 20%">
                        <p class="text-muted">
                            <span class="card-currency" v-for="im of item.currency">{{im}}</span>
                            <!--<span class="card-currency">LTC</span>-->
                            <!--<span class="card-currency">ETH</span>-->
                            <!--<span class="card-currency">DASH</span>-->
                            <!--<span class="card-currency">XRP</span>-->
                            <!--<span class="card-currency">ZEC</span>-->
                        </p>
                    </div>
                </el-card>
            </el-col>
        </el-row>
    </div>
</template>

<script>
    export default {
        name: "buy",
        data(){
            return{
                items:[
                ]
            }
        },
        created() {
            this.getData();
        },
        methods:{
            getData() {
                this.$axios.get("./static/bay.json").then((res) => {
                    this.items = res.data.list;
                })
            },
        }
    }
</script>

<style scoped>
.bank_transfer{
    display: flex;
    flex-direction: column;
    cursor: pointer;
    margin-bottom: 16px;
    border-radius: 0;
    border: unset;
    height: 300px;
    outline: 1px solid #ddd;
}
.logo{
    padding-top: 15px;
    height: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
}
.card-block{
    display: flex;
    flex-direction: column;
    flex: 1;
    padding: 15px;
}
    .card-title{
        margin-top: 10px;
        margin-bottom: 15px;
        text-align: center;
    }
    .text-muted{
        text-align: center;
        color: #777777;
    }
    hr{
        margin-top: 17px;
        margin-bottom: 17px;
        border: 0;
        border-top: 1px solid #eeeeee;
    }
    .card-currency{
        display: inline-block;
        color: #848484;
        padding: 2px 6px;
        font-size: 11px;
        border-radius: 2px;
        font-weight: 600;
        border: 1px solid #bcbcbc;
        margin: 0 2px 4px;
    }
</style>
