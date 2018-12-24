<template>
    <div class="sell" id="sell">
        <div class="title">Sell Bitcoin</div>
        <el-row :gutter="20">
            <el-col :span="14" :offset="5">
                <el-form :model="sellForm" :rules="sellRules" ref="sellForm" label-width="100px" class="demo-ruleForm">
                    <el-form-item label="Payout to:">
                        <div>1 {{currency1}} = {{rate}} {{currency2}}</div>
                    </el-form-item>
                    <el-form-item label="Pay with:">
                        <!--prop="payWith"-->
                        <el-input @input="currencyInputChange()" placeholder="The amount of BCH you wish to sell" v-model="sellForm.payWith" class="input-with-select">
                            <el-select @change="currencyChange(sellForm.select,sellForm.payWith,sellForm.receive)" style="width: 130px" v-model="sellForm.select" slot="prepend" placeholder="请选择">
                                <el-option label="BTC" value="BTC">Bitcoin</el-option>
                                <el-option label="LTC" value="LTC">Litecoin</el-option>
                                <el-option label="ETH" value="ETH">Ethereum</el-option>
                                <el-option label="BCH" value="BCH">Bitcoin Cash</el-option>
                            </el-select>
                        </el-input>
                        <!--<el-input v-model="sellForm.payWith"></el-input>-->
                    </el-form-item>
                    <el-form-item label="Receive:">
                        <!--prop="payWith"-->
                        <el-input @input="currency2InputChange()" placeholder="The amount of EUR you will get" v-model="sellForm.receive" class="input-with-select">
                            <el-select style="width: 130px" v-model="sellForm.selectReceive" slot="prepend" placeholder="请选择">
                                <el-option label="EUR" value="EUR">EURO</el-option>
                                <!--<el-option label="LTC" value="2">Litecoin</el-option>-->
                                <!--<el-option label="ETH" value="3">Ethereum</el-option>-->
                                <!--<el-option label="BCH" value="4">Bitcoin Cash</el-option>-->
                            </el-select>
                        </el-input>
                        <!--<el-input v-model="sellForm.payWith"></el-input>-->
                    </el-form-item>

                    <el-form-item label="Payout to:">
                        <el-button type="danger" plain icon="el-icon-circle-plus">Add Euro payout address</el-button>
                    </el-form-item>

                </el-form>
            </el-col>
        </el-row>
    </div>
</template>

<script>
    export default {
        name: "sell",
        data(){
            return{
                currency1:"BTC",
                currency2:"EUR",
                rate:"",
                sellForm:{
                    payWith:"",
                    select:"BTC",
                    receive:"",
                    selectReceive:"EUR"
                },
                sellRules:{
                    payWith:[
                        { required: true, message: '请输入活动名称', trigger: 'blur' }
                    ]
                }
            }
        },
        methods:{
            currencyChange(data1){
                if(data1 != this.currency1){
                    this.currency1 = data1;
                    this.rate=Math.floor(Math.random() * (500 - 100 + 1)) + 100;
                    this.sellForm.receive=this.sellForm.payWith*this.rate;
                }
            },
            currencyInputChange(){
                this.sellForm.receive=this.sellForm.payWith*this.rate;
            },
            currency2InputChange(){
                this.sellForm.payWith=this.sellForm.receive/this.rate;
            }
        },
        created(){
            this.rate=Math.floor(Math.random() * (500 - 100 + 1)) + 100;
        },
        filters: {
            num: function (value) {
                if (!value) return "";
                value = value.toFixed(2);
                return value
            }
        },
        computed:{

        }
    }
</script>

<style scoped>
    .sell .title{
        margin: 10px 0px;
        color: #777;
        font-size: 14px;
    }
   #sell .el-input--small .el-input__inner {
        height: 40px !important;
        line-height: 40px !important;
    }
</style>
