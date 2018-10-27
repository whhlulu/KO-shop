<template>
    <div class="new-list-scroll">
        <new-list :newList="$store.state.homeNewList"></new-list>
        <div class="comm-null" v-if="$store.state.homeNewList.length===0">
            <div class="con-wrap text-center">
                <img src="../../assets/null_com.png">
                <p>暂时没有商品</p>
            </div>
        </div>
        <p class="page-infinite-loading" v-show="$store.state.KOhomequeryLoading">
            <mt-spinner type="fading-circle" color="#666" :size="20" v-show="$store.state.KOhomemoreLoading"></mt-spinner>
            <span style="font-size:.2rem;color:#666;" v-show="$store.state.KOhomeallLoaded">暂无更多数据</span>
            <span style="font-size:.2rem;color:#666;" v-show="$store.state.KOhomeloading">加载中...</span>
        </p>
    </div>
</template>
<script>
    import {MessageBox, Toast} from 'mint-ui';
    import newList from './children/newList.vue'
    import qs from 'qs';
    export default {
        name: 'newListScroll',
        data(){
            return {
                scrollWatch: true,
            }
        },
        components: {
            newList,
        },
        mounted() {
//            document.body.scrollTop = 0;
            this.$store.state.KOhomepage = 1;
            this.$store.state.KOhomequeryLoading = false;
            this.$store.state.KOhomeallLoaded = false;
            this.$store.state.KOhomemoreLoading = false;
            this.$store.state.KOhomeloading = false;
            this.$store.state.KOhomeno_data = false;
            this.$store.state.KOhomeslidingSwitch = true;
            this.getOrderList();
            let this_ = this;
            // 注册scroll事件并监听
            var n = 100;
            window.addEventListener('scroll', () => {
                if (this_.scrollWatch) {
                    // 判断是否滚动到底部
                    if (document.body.scrollTop + window.innerHeight + 50 >= document.body.offsetHeight) {
                        if (this_.$store.state.KOhomeno_data === true) {
                            return false;
                        }
                        // 如果开关打开则加载数据
                        if (this_.$store.state.KOhomeslidingSwitch == true) {
                            this_.$store.state.KOhomeslidingSwitch = false;
                            if (this_.$store.state.KOhomeallLoaded === true) {
                                return false;
                            } else {
                                this_.$store.state.KOhomepage++;
                                this_.$store.state.KOhomequeryLoading = true;
                                this_.$store.state.KOhomemoreLoading = true;
                                this_.$store.state.KOhomeloading = true;

                                setTimeout(() => {
                                    this_.$store.state.KOhomeslidingSwitch = true;
                                    var data = [
                                        {id: (n + 1), title: '1',},
                                        {id: (n + 2), title: '2',},
                                        {id: (n + 3), title: '3',},
                                        {id: (n + 4), title: '4',},
                                        {id: (n + 5), title: '5',},
                                    ]
                                    data.forEach(function (val, index) {
                                        this_.$store.state.homeNewList.push(val);
                                    });
                                    n = n + 20;
                                }, 2000)

//                                this.axios({
//                                    url:API_URL + 'Home/Order/myOrder',
//                                    method:'get',
//                                    params:{
//                                        app_user_id:sessionStorage.getItem('user_ID'),
//                                        order_status:this.$store.state.order_status,
//                                        p:this_.$store.state.page
//                                    }
//                                }).then((res) => {
//                                    this_.$store.state.slidingSwitch = true;
//                                    if(res.data.status == 0){
//                                        this_.$store.state.moreLoading = false;
//                                        this_.$store.state.allLoaded = true;
//                                        this_.$store.state.loading = false;
//                                        return false;
//                                    }
//                                    res.data.data.forEach(function(val,index){
//                                        this_.$store.state.order.push(val);
//                                        });
//                                }).catch((err) => {
//                                    console.log(err);
//                                });
                            }

                        }
                    }
                }

            });
        },
        destroyed(){
            this.scrollWatch = false;
        },
        methods: {
            getOrderList(){
                var this_ = this;
                var data = [
                    {id: 1, title: '爱仕达1',pic_url:'',state:'',company:'百度新闻是包含海量资讯的新闻服务平台,真实反映每时每刻的新闻热点。您可以搜索新闻事件、'},
                    {id: 2, title: 'sasd2',pic_url:'',state:'',company:'ssss'},
                    {id: 3, title: 'asd3',pic_url:'',state:'',company:'ssss'},
                    {id: 4, title: '4',pic_url:'',state:'',like:true},
                    {id: 5, title: '5',pic_url:'',state:'',like:false},
                    {id: 6, title: '5',pic_url:'',state:''},
                    {id: 7, title: '5',pic_url:'',state:''},
                    {id: 8, title: 'asd5',pic_url:'',state:''},
                    {id: 9, title: 'asd5',pic_url:'',state:''},
                    {id: 10, title: 'asd5',pic_url:'',state:''},
                ]
                data.forEach(function (val, index) {
                    this_.$store.state.homeNewList.push(val);
                });
                if (data.length < 10) {
                    this.$store.state.KOhomeno_data = true;
                }
//                this.axios({
//                        url:API_URL + 'Home/Order/myOrder',
//                        method:'get',
//                        params:{
//                            app_user_id:sessionStorage.getItem('user_ID'),
//                            order_status:this.$store.state.order_status,
//                            p:this.$store.state.page
//                        }
//                    }).then((res) => {
//                        this.$store.state.order = res.data.data;
//                        if(res.data.data.length<10){this.$store.state.no_data = true;}
//                        this.$store.state.order_load_wrap = false;
//                    }).catch((err) => {
//                        console.log(err);
//                    });
            },
        }
    }
</script>
<style lang="less">
    .page-infinite-loading {
        span {
            .mint-spinner-fading-circle {
                display: inline-block;
                vertical-align: middle;
                margin-right: 5px;
            }
        }

    }
</style>

<style lang="less" scoped>
    .new-list-scroll {
        .comm-null {
            padding-top: .5rem;
            p {
                font-size: .28rem;
                color: #666;
                padding-top: .2rem;
            }
        }
        .page-infinite-loading {
            text-align: center;
            height: 30px;
            line-height: 30px;
        }
    }
</style>