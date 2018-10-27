<template>
    <div class="per-center">
        <div v-title data-title="个人中心">个人中心</div>
        <div class="header-wrap">
            <div class="header-hd">个人中心<router-link to="/myNews"><span></span></router-link></div>
            <div class="header-dd-center">
                <!--<div class="setUp"></div>-->
                <div class="icon-wrap" @click="toLink('/seetin')">
                    <img v-if="data.user_header" :src="URL+ data.user_header">
                    <img v-else src="../../assets/my_user_pic.png">
                </div>
                <div class="admin" @click="toLink('/seetin')"><span></span>账户管理</div>
            </div>
            <div class="status">
                <span class="name">{{data.user_name}}</span>
                <span class="member">{{data.level_name}}</span>
            </div>
        </div>
        <ul class="more clearfix">
            <li class="fl" v-for="(item,index) in more.icon" :key="item.id" @click="toLink(index)">
                <div class="icon-main">
                    <img :src="item">
                </div>
                <p>{{more.name[index]}}</p>
            </li>
        </ul>
    </div>
</template>
<script>
    import qs from 'qs';
    import '../../config/getUrlParm.js';
    export default {
        name : 'MyAiguxuan',
        data(){
            return {
                more:{
                     name:['我的收藏','足迹','客服中心','意见反馈'],
                    icon:[
                        require('@/assets/images/collection.png'),
                        require('@/assets/images/footprint.png'),
                        require('@/assets/images/service.png'),
                        require('@/assets/images/opinion.png'),
                    ],
                },
                Imag:'',
                data:'',
                user_header:true
            }
        },
        destroyed(){
        },
        components: {
        },
        methods:{
        	toOrder_list(){
        		this.$router.push({
                    name:'orderList',
                    params:{id:0}
                });
        	},
            toOrder(sat){
            	if(sat==0){
            		this.$router.push({
	                    name:'orderList',
	                    params:{id:1}
	                });
            	}else if(sat==1){
            		this.$router.push({
	                    name:'orderList',
	                    params:{id:2}
	                });
            	}else if(sat==2){
            		this.$router.push({
	                    name:'orderList',
	                    params:{id:3}
	                });
            	}else if(sat==3){
            		this.$router.push({
	                    name:'orderList',
	                    params:{id:4}
	                });
            	}else if(sat==4){
            		this.$router.push('/repair')
                    return;
            	}
            },
            toLink(link){
                function isString(str){ 
                    return (typeof str=='string')&&str.constructor==String; 
                };
                if(isString(link)){
                    this.$router.push({
                        path:link
                    });
                }else{
                    switch(link){
                        case 0:
                            this.$router.push('/coupon');
                            break;
                        case 1:
                            this.$router.push('/Integral')
                            break;
                        case 2:
                            this.$router.push('/Collection');
                            break;
                        case 3:
                            this.$router.push('/footprint')
                            break;
                        case 5:
                            this.$router.push('/myWallet')
                            break;
                        case 6:
                            this.$router.push('/documents')
                            break;
                        case 7:
                            this.$router.push('/shopOpen')
                            break;
                        case 8:
                            this.$router.push('/myComment')
                            break;
                        case 9:
                            this.$router.push({
                                name:'address',
                                params:{
                                    status:2
                                }
                            });
                            break;
                        case 10:
                            this.$router.push('/customer');
                            break;
                        case 11:
                            this.$router.push('/Feedback');
                            break;
                        case 12:
                            this.$router.push({
                                name:'packageList',
                                params:{
                                    id:0
                                    }
                            });
                            break;
                        case 13:
                            this.$router.push('/intOrder');
                            break;
                    }
                }
            }
        },
        created(){
        },
        mounted(){
        	document.body.scrollTop = 0;
        	
            this.axios.post(
                this.$httpConfig.userinfo
            ).then((res) => {
            	if(res.data.status==10001){
		            this.$router.push('/LogIn');
		        } else{
                    this.data = res.data.data;
                    let ua = window.navigator.userAgent.toLowerCase();
                    if (ua.match(/MicroMessenger/i) == 'micromessenger') {
                        this.$store.state.user_Imag=res.data.data.weixheader
                    } else {
                        this.$store.state.user_Imag=res.data.data.user_header
                    }
                    
		        }
            }).catch((err) => {
                console.log(err)
            });
        },
        wacth:{
            
        }
    }
</script>
<style lang="less" scoped>
    .per-center{
        background:#f1f1f1;
    }
    .header-wrap{
        width:100%;
        background: -webkit-linear-gradient(left, #D29F2C, #EFB93F);
        background: -o-linear-gradient(right, #D29F2C, #EFB93F);
        background: -moz-linear-gradient(right,#D29F2C, #EFB93F);
        background: linear-gradient(to right, #D29F2C, #EFB93F);
        .header-hd{
            height:.6rem;
            line-height:.6rem;
            font-size:.32rem;
            padding:.2rem 0;
            color:#fff;
            text-align:center;
            position:relative;
            span{
                width:.47rem;
                height:.46rem;
                position:absolute;
                right:.23rem;
                top:50%;
                margin-top:-.23rem;
                background:url('../../assets/news1.png') no-repeat;
                background-size:100% 100%;
            }
        }
        .header-dd-center{
            width:100%;
            height:1.5rem;
            position:relative;
            .setUp{
                width:.62rem;
                height:.61rem;
                position:absolute;
                left:1.04rem;
                top:50%;
                margin-top:-.305rem;
                background:url(../../assets/setUp.png) no-repeat;
                background-size:100% 100%;
            }
            .icon-wrap{
                width:1.26rem;
                height:1.26rem;
                border:.09rem solid #DEBC62;
                border-radius:100%;
                overflow:hidden;
                position:absolute;
                left:0;
                top:0;
                right:0;
                bottom:0;
                margin:auto;
                img{
                    width:1.26rem;
                    height:1.26rem;
                    border-radius:100%;
                    box-sizing:border-box;
                }
            }
            .admin{
                height:.61rem;
                width:1.68rem;
                line-height:.61rem;
                background:#fff;
                position:absolute;
                right:0;
                top:50%;
                margin-top:-.305rem;
                border-radius:20px 0 0 20px;
                box-sizing:border-box;
                text-indent:.53rem;
                font-size:.24rem;
                color:#797979;
                span{
                    position:absolute;
                    top:50%;
                    left:.15rem;
                    margin-top:-.135rem;
                    width:.27rem;
                    height:.27rem;
                    background:url(../../assets/images/setUp.png) no-repeat;
                    background-size:100% 100%;
                }
            }
        }
        .status{
            padding:.2rem 0;
            text-align:center;
            line-height:.31rem;
            span{
                display:inline-block;
                height:.31rem;
            }
            .name{
                font-size:.28rem;
                color:#fff;
            }
            .member{
                padding-left:.37rem;
                padding-right:.1rem;
                width:1.08rem;
                font-size:.24rem;
                color:#fff600;
                background:url(../../assets/mberIcon.png) no-repeat;
                background-size:100% 100%;
            }
        }
    }
 .more{
        border-top:1px solid #dfdfdf;
        background:#fff;
        li{
            width:25%;
            height:2rem;
            border-right:1px solid #ebebeb;
            border-bottom:1px solid #ebebeb;
            box-sizing: border-box;
            text-align:center;
            p{
                font-size:.24rem;
                color:#333;
            }
            .icon-main{
                width:100%;
                height: .86rem;
                position:relative;
                padding-top:.57rem;
            }
            &:nth-child(1){
                img{
                    width:.46rem;
                    height:.5rem;
                }
            }
            &:nth-child(2){
                img{
                    width:.45rem;
                    height:.55rem;
                }
            }
            &:nth-child(3){
                img{
                    width:.61rem;
                    height:.57rem;
                }
            }
            &:nth-child(4){
                img{
                    width:.48rem;
                    height:.48rem;
                }
            }
            &:nth-child(4n){
                border-right:none;
            }
        }
    }
</style>