<template>
    <div>
       <nav-header></nav-header>
        <nav-bread>
            <span slot="bread">Goods</span>
        </nav-bread>
        <div class="accessory-result-page accessory-page">
            <div class="container">
                <div class="filter-nav">
                    <span class="sortby">Sort by:</span>
                    <a href="javascript:void(0)" class="default cur">Default</a>
                    <a href="javascript:void(0)" class="price">Price <svg class="icon icon-arrow-short"><use xlink:href="#icon-arrow-short"></use></svg></a>
                    <a href="javascript:void(0)" class="filterby stopPop" @click="showFilterPop">Filter by</a>
                </div>
                <div class="accessory-result">
                <!-- filter -->
                <div class="filter stopPop" id="filter" v-bind:class="{'filterby-show':filterBy}">
                    <dl class="filter-price">
                    <dt>Price:</dt>
                    <dd>
                        <a href="javascript:void(0)" v-bind:class="{'cur':priceCheck=='all'}" @click = "setPriceFilter('all')">All</a>
                    </dd>
                    <!-- 循环读取出价格的区间 -->
                    <dd v-for="(item,index) in priceFilter" >
                        <a href="javascript:void(0)" @click = "setPriceFilter(index)"  v-bind:class="{'cur':priceCheck==index}">{{item.startPrice}} - {{item.endPrice}}</a>
                    </dd>
                    </dl>
                </div>
       
                <!-- search result accessories list -->
                <div class="accessory-list-wrap">
                    <div class="accessory-list col-4">
                    <ul>
                        <!-- 循环读取出购物车和图片的内容 -->
                        <li v-for="(item,index) in goodList">
                            <div class="pic">
                                <a href="#">
                                    <img v-lazy="'/static/'+item.productImg" alt="">
                                </a>
                            </div>
                            <div class="main">
                                <div class="name">{{item.productName}}</div>
                                <div class="price">{{item.productPrice}}</div>
                                <div class="btn-area">
                                <a href="javascript:;" class="btn btn--m">加入购物车</a>
                                </div>
                            </div>
                        </li>
                    </ul>
                    </div>
                </div>
                </div>
            </div>
        </div>
        <div class="md-overlay" v-show="overLayFlag" @click="closePop"></div>
        <nav-footer></nav-footer>
    </div>
</template>
<script>
    import "./../assets/css/base.css";
    import "./../assets/css/product.css";
    import NavHeader from "./NavHeader.vue";
    import NavFooter from "@/views/NavFooter.vue";
    import NavBread from "./NavBread.vue";
    import axios from "axios";
    export default {
        data(){
            return{
                goodList:[],
                priceFilter:[
                    {
                        startPrice:"0.00",
                        endPrice:"100.00"
                    },
                    {
                        startPrice:"100.00",
                        endPrice:"500.00"
                    },
                    {
                        startPrice:"500.00",
                        endPrice:"1000.00"
                    },
                    {
                        startPrice:"1000.00",
                        endPrice:"2000.00"
                    }
                ],
                priceCheck:"all",
                filterBy:false,
                overLayFlag:false,
            }
        },
        components:{
            NavHeader,
            NavFooter,
            NavBread
        },
        mounted:function(){
            this.getGoodList();
        },
        methods:{
            getGoodList(){
                axios.get("https://www.easy-mock.com/mock/5c134d091ed4e34c5e134742/example_copy_copy/goods").then( (result)=>{
                    var res = result.data;
                    this.goodList = res.result;
                });
            },
            // 控制弹出
            showFilterPop(){
                this.filterBy = true;
                this.overLayFlag = true;
            },
            // 控制隐藏
            closePop(){
                this.filterBy = false;
                this.overLayFlag = false;
            },
            setPriceFilter(index){
                this.priceCheck = index;
                this.filterBy = false;
                this.overLayFlag = false;
            }
        }
    }
</script>
