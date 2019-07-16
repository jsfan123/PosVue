<template>
    <div class="left-nav">
        <ul>
            <li>
                <i class="icon iconfont icon-jiezhang"></i>
                <div class="left-icon">收银</div>
            </li>
            <li>
                <i class="icon iconfont icon-dianpu"></i>
                <div class="left-icon">店铺</div>
            </li>
            <li>
                <i class="icon iconfont icon-hanbao"></i>
                <div class="left-icon">商品</div>
            </li>
            <li>
                <i class="icon iconfont icon-huiyuan"></i>
                <div class="left-icon">会员</div>
            </li>
            <li>
                <i class="icon iconfont icon-jisuan"></i>
                <div class="left-icon">统计</div>
            </li>
            <li>
                <i class="icon iconfont icon-shezhi"></i>
                <div class="left-icon">设置</div>
            </li>
        </ul>
    </div>
</template>
<script>
export default {
   
}
</script>
<style>
 .left-nav{
     color: #fff;
     font-size: 10px;
     height: 100%;
     background-color: #1d8ce0;
     float: left;
     width: 5%;

 }
 .iconfont{
     font-size: 20px;
 }
 .left-nav ul{
     margin: 0px;
     padding: 0;
 }
 .left-nav li{
     list-style: none;
     text-align: center;
     border-bottom: 1px solid #20a0ff;
     padding: 10px 10px;
 }
 /* 设置左侧导航图标与文字的上下距离 */
  .left-nav li .left-icon{
     margin-top: 5px;
 }
</style>
