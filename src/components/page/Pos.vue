<template>
    <div class="pos">
        <el-row>
            <!-- 订单栏 -->
            <el-col :span='7' :xs='12' class="list-main" id="listLeft">
                <template>
                    <div>
                        <el-tabs stretch>
                            <el-tab-pane label="订单" >
                                <template>
                                    <el-table :data="tableData" style="width:100%" border >
                                        <el-table-column prop="goodsName" label="商品名称" width="120" align='center'></el-table-column>
                                        <el-table-column prop="count" label="数量" width="70" align='center'></el-table-column>
                                        <el-table-column prop="price" label="单价" width="70" align='center'></el-table-column>
                                        <el-table-column label="操作" fixed="right" align='center'>
                                            <!-- 从2.5版本后用slot-scope来代替scope -->
                                            <template slot-scope="scope" class="addhreduce">
                                                <!-- 删除单个商品 -->
                                                <el-button type="text" @click='deleteSingle(scope.row)'>删除</el-button>
                                                <!-- scoped.row 就是把当前行的数据获取到 -->
                                                <el-button type="text" @click='addGoods(scope.row)'>添加</el-button>
                                            </template>
                                        </el-table-column>
                                    </el-table>
                                </template>
                                <!-- 订单栏的商品总数和金额 -->
                                <div class="totalData">
                                    <div class="totalChild">
                                        <span class="total-money"><small>总数：</small><b>{{totalCount}} </b><small>个</small></span>
                                        <span class="total-count"><small>金额：</small><b>{{totalMoney}} </b><small>元</small></span>
                                    </div>
                                </div>

                                <!-- 订单页的按钮 -->
                                <template scoped="scoped">
                                    <div class="list-btn">
                                        <el-button type="success" @click="jiezhang">结账</el-button>
                                        <el-button type="warning">挂单</el-button>
                                        <el-button type="danger" @click="deleteAll">删除</el-button>
                                    </div>
                                </template>
                            </el-tab-pane>
                            <el-tab-pane label="挂单"></el-tab-pane>
                            <el-tab-pane label="外卖"></el-tab-pane>
                        </el-tabs>
                    </div>
                   
                </template>
                
            </el-col>
            <!-- 我是产品栏 -->
            <el-col :span='17' :xs='12'>
                <div class="often-goods">
                    <div class="title">常用商品</div>
                    <div class="goods-list">
                        <ul>
                            <li v-for="goods in oftenGoods" :key='goods.goodsName' @click='addGoods(goods)'>
                                <span>{{goods.goodsName}}</span>
                                <span class="o-price">{{goods.price}}￥</span>
                            </li>
                        </ul>
                    </div>
                </div>

                <!-- 商品分类布局 -->
                <div class="goods-type">
                    <el-tabs stretch>
                        <el-tab-pane label="汉堡">
                            <div>
                                <ul class="goodsList">
                                    <li v-for="(goods,index) in type0Goods" :key='index' @click='addGoods(goods)'>
                                        <!-- src="../../assets/img/1.jpg" 本地图片地址  :src="goods.goodsImg" ;服务器失效图片地址-->
                                        <span class="foodImg"><img src="../../assets/img/1.jpg" width="100%"></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}</span>
                                    </li>
                                </ul>
                            </div>
                        </el-tab-pane>
                        <el-tab-pane label="小吃">
                            <div>
                                <ul class="goodsList">
                                    <li v-for="(goods,index) in type1Goods" :key='index' @click='addGoods(goods)'>
                                        <!-- src="../../assets/img/1.jpg" 本地图片地址  :src="goods.goodsImg" ;服务器失效图片地址-->
                                        <span class="foodImg"><img src="../../assets/img/1.jpg" width="100%"></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}</span>
                                    </li>
                                </ul>
                            </div>
                        </el-tab-pane>
                        <el-tab-pane label="饮品">
                            <div>
                                <ul class="goodsList">
                                    <li v-for="(goods,index) in type2Goods" :key='index' @click='addGoods(goods)'>
                                        <!-- src="../../assets/img/1.jpg" 本地图片地址  :src="goods.goodsImg" ;服务器失效图片地址-->
                                        <span class="foodImg"><img src="../../assets/img/1.jpg" width="100%"></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}</span>
                                    </li>
                                </ul>
                            </div>
                        </el-tab-pane>
                        <el-tab-pane label="套餐">
                            <div>
                                <ul class="goodsList">
                                    <li v-for="(goods,index) in type3Goods" :key='index' @click='addGoods(goods)'>
                                        <!-- src="../../assets/img/1.jpg" 本地图片地址  :src="goods.goodsImg" ;服务器失效图片地址-->
                                        <span class="foodImg"><img src="../../assets/img/1.jpg" width="100%"></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}</span>
                                    </li>
                                </ul>
                            </div>
                        </el-tab-pane>
                        
                    </el-tabs>
                </div>
            </el-col>
        </el-row>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name:'pos',
    // 在vue实例一创建就开始取数据
    created:function(){
        // 利用axios获取常用商品的数据
        axios.get('https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/oftenGoods')
        .then(response=>{
            // console.log(response)
            this.oftenGoods = response.data
        })
        .catch(error=>{
            console.log(error);
            alert('网络异常，请检查网络是否连接！')
        })
        // 利用axios获取分类商品1的数据
        axios.get('https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/typeGoods')
        .then(response=>{
            // console.log(response);
            this.type0Goods = response.data[0];
            this.type1Goods = response.data[1];
            this.type2Goods = response.data[2];
            this.type3Goods = response.data[3];
        })
        .catch(error=>{
            console.log(error)
            alert("网络异常，请检查网络是否连接！")
        })
    },
    // 通过原生js来设置订单栏的100%宽高
    mounted:function(){
        function setHeight(){
            var listLeft = document.getElementById("listLeft");
            var domHeight = document.documentElement.clientHeight;
            listLeft.style.height = domHeight + 'px';
        }
        setHeight();
        window.onresize = function(){
           setHeight();
        }
    },
    data() {
      return {
        //  订单总价和总数
        totalMoney:0,
        totalCount:0,
        // 订单栏的数据
        tableData:[],
        oftenGoods:[],
        type0Goods:[],
        type1Goods:[],
        type2Goods:[],
        type3Goods:[],
      };
    },
    // 实现点击常用商品和分类商品能添加到左侧的商品栏
    methods:{
        // 添加商品的方法
        addGoods(goods){

            // 每次添加都先把之前的订单状态清空
            this.totalMoney = 0;
            this.totalCount = 0;
            let isHave = false
            // 利用循环遍历判断在左侧订单栏是否存在该商品
            this.tableData.forEach(g=>{
                if(g.goodsId == goods.goodsId){
                    isHave = true;
                }
            })

            // 如果商品存在就直接把数量加一，否则添加商品到订单栏
            if(isHave){
                // 存在就进行数量增加
                // 过滤返回的是一个数组
                let arr = this.tableData.filter(g=>g.goodsId == goods.goodsId)
                // 所以让数组的第一项里面的count++就行了
                arr[0].count++;

            }else{
                console.log(goods)
                // 如果不存在就添加商品到订单栏
                let newGoods = {goodsId:goods.goodsId,goodsName:goods.goodsName,price:goods.price,count:1}
                // 再把这个对象添加到tableData数据中
                this.tableData.push(newGoods);
            }

            // 在每次点击添加之后都把每个商品的总数和价格加起来汇总
            this.ComputedCount();
            
        },
        // 删除单个商品的功能
        deleteSingle(goods){
            let arr = this.tableData.filter(g=>g.goodsId == goods.goodsId);
            arr[0].count--;

            if(!arr[0].count){
               this.tableData = this.tableData.filter(g=>g.goodsId != goods.goodsId);
            }
            // 每删除一个商品就调用一次计算总价和总数的函数
            this.ComputedCount();
        },
        // 模拟结账
        jiezhang(){
            this.totalMoney = 0;
            this.totalCount = 0;
            this.tableData = [];
            this.$notify({
                title:'结账成功',
                message:'感谢您的消费，欢迎下次光临！',
                duration:2400,
                offset:100,
                type:'success'
            })
        },
        // 删除整个订单信息
        deleteAll(){
            if(this.totalCount == 0){
                console.log("错了哦，这是一条错误消息")
                this.$notify.error({
                    title:'删除',
                    message:'你还没有点餐呢，老板！',
                    type:'error',
                    // position:'top-left',
                    offset: 100,
                    duration:2400
                });
            }
            this.totalMoney = 0;
            this.totalCount = 0;
            this.tableData = [];
        },
        // 计算总价和总量
        ComputedCount(){
            this.totalMoney = 0;
            this.totalCount = 0;
            this.tableData.forEach(element=>{
                this.totalCount += element.count;
                this.totalMoney += (element.count*element.price);
            })
        }
    }
   
}
</script>
<style>
    
    /* 订单栏样式 */
    .list-main{
        border-right:1px solid #d3dce6; 
        background-color: #fff;
    }
    .list-btn{
        margin-top: 20px;
    }
    .list-main .totalData{
        padding: 20px 50px;
        background-color: #fff;
        border-bottom:1px solid #d3dce6;
    }
    .totalChild span{
        display: inline-block;
        text-align: left;
        width: 40%;
        text-align: center;
    }
    .totalChild b{
        color: #f60;
    }
    
    /* 常用商品样式 */
    .often-goods .title{
        height: 20px;
        background-color: #fff; 
        padding: 10px;
        border-bottom:1px solid #D3DCE6;
        text-align: left;
    }
    .often-goods .goods-list li{
        list-style: none;
        background-color:#fff; 
        float: left;
        box-shadow:  0 3px 4px rgba(0, 0, 0, .12), 0 0 6px rgba(0, 0, 0, .04);
        padding: 10px;
        margin: 10px;
        border-radius: 4px;
        cursor: pointer;
    }
    .goods-list li span{
        color: #555;
    }
    .goods-list li .o-price{
        color: #00b5e5;
        font-weight: bold;
    }

    .goods-type{
        clear: both;
    }
    .goosList{
        overflow: hidden;
    }
    .goodsList li{
       list-style: none;
       width:23%;
       border:1px solid #E5E9F2;
       height: auot;
       overflow: hidden;
       background-color:#fff;
       padding: 5px;
       float:left;
       margin: 10px;
       box-shadow: 0 3px 4px rgba(0, 0, 0, .12), 0 0 6px rgba(0, 0, 0, .04);
       border-radius: 5px; 
       cursor: pointer;
    }
   .goodsList li span{
        display: inline-block;
        float: left;
   }
    .foodImg{
       width: 40%;
   }
   .foodName{
       width: 50%;
       font-size: 18px;
       padding: 10px 0 0 10px;
       vertical-align: middle;
       text-align: left;
       color: #555;
       white-space: nowrap;
       text-overflow: ellipsis;
       overflow: hidden;
 
   }
   .foodPrice{
       font-size: 20px;
       padding-left: 10px;
       padding-top:8px;
       color:#f60;
       font-weight: bold;

   }
</style>
