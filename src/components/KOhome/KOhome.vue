<template>
    <div class="KOhome">
        <!--<div class="load-wrap" v-show="$store.state.load_wrap" @touchmove.prevent>-->
            <!--<mt-spinner type="triple-bounce" color="rgb(38, 162, 255)"></mt-spinner>-->
        <!--</div>-->
        <div v-title data-title="主页">主页</div>
        <home-header :userName="getData"></home-header>
        <mt-swipe :auto="4000">
            <mt-swipe-item v-for="(item,index) in $store.state.lunboList" :key="item.id">
                <img v-lazy="item.pic_url">
            </mt-swipe-item>
        </mt-swipe>
        <news-flash :nav="$store.state.fenlei"></news-flash>
        <hot-goods :data="$store.state.zixunList"></hot-goods>
    </div>
</template>
<script>
    import HomeHeader from './children/Header';
    import NewsFlash from './children/newsFlash';
    import hotGoods from './children/hotGoods';
    export default {
        name: 'KOhome',
        data() {
            return {
                getData:'',
            }
        },
        created() {
            //是否登陆过
            let userid  =  localStorage.getItem('user_ID');
            if(userid){
                sessionStorage.setItem('user_ID', userid);
            }
            var userName = this.$route.params.userName;
            this.getData = userName;

            //
            this.$store.state.lunboList = [
                {id:1,pic_url:'http://center.shopsn.cn/Uploads/ad/2018-06-08/5b1a164b06c5b.jpg'},
                {id:2,pic_url:'http://center.shopsn.cn/Uploads/ad/2018-06-08/5b1a18c3e6fa0.jpg'},
            ];
            this.$store.state.fenlei = [
                {id:1,nav_titile:'安全',nav_img:'http://center.shopsn.cn/Uploads/ad/2018-06-08/5b1a18c3e6fa0.jpg'},
                {id:2,nav_titile:'分类',nav_img:'http://center.shopsn.cn/Uploads/ad/2018-06-08/5b1a18c3e6fa0.jpg'},
                {id:3,nav_titile:'地震',nav_img:'http://center.shopsn.cn/Uploads/ad/2018-06-08/5b1a18c3e6fa0.jpg'},
                {id:4,nav_titile:'食品',nav_img:'http://center.shopsn.cn/Uploads/ad/2018-06-08/5b1a18c3e6fa0.jpg'},
                {id:5,nav_titile:'健康',nav_img:'http://center.shopsn.cn/Uploads/ad/2018-06-08/5b1a18c3e6fa0.jpg'},
                {id:6,nav_titile:'运动',nav_img:'http://center.shopsn.cn/Uploads/ad/2018-06-08/5b1a18c3e6fa0.jpg'},
            ];
            this.$store.state.zixunList = [
                {id:1,title:'安全',pic_url:'http://center.shopsn.cn/Uploads/ad/2018-06-08/5b1a18c3e6fa0.jpg',price_market:'12'},
                {id:2,title:'分类',pic_url:'http://center.shopsn.cn/Uploads/ad/2018-06-08/5b1a18c3e6fa0.jpg',price_market:'12'},
                {id:3,title:'地震',pic_url:'http://center.shopsn.cn/Uploads/ad/2018-06-08/5b1a18c3e6fa0.jpg',price_market:'12'},
                {id:4,title:'食品',pic_url:'http://center.shopsn.cn/Uploads/ad/2018-06-08/5b1a18c3e6fa0.jpg',price_market:'12'},
                {id:5,title:'健康',pic_url:'http://center.shopsn.cn/Uploads/ad/2018-06-08/5b1a18c3e6fa0.jpg',price_market:'12'},
                {id:6,title:'运动',pic_url:'http://center.shopsn.cn/Uploads/ad/2018-06-08/5b1a18c3e6fa0.jpg',price_market:'12'},
            ];
        },
        methods:{

        },
//        updated(){
//            var that = this;
//            setTimeout(function(){
//                that.$store.state.load_wrap = false;
//            },1000);
//        },
        components: {
            HomeHeader,
            NewsFlash,
            hotGoods,
        }
    }
</script>
<style lang="less">
    .KOhome{
        .mint-swipe-indicators{
            width: 100%;
            text-align: center;
        }
    }
</style>
<style lang="less" scoped>
.KOhome{
    .mint-swipe{
        width:100%;
        height:3.28rem;
        img{
            width:100%;
            height:100%;
        }
        .mint-swipe-indicators{
            .mint-swipe-indicator{
                width:20px;
                height:20px;
            }
        }
    }
}
</style>