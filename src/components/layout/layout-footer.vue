<template>
    <div id="layout-footer" class="home">
        <div class="footer-main">
            <div class="footer-item" v-if="socials.length">
                <div v-for="item in socials" :key="item.id"><a target="_blank" class="out-link" :href="item.href"><i class="iconfont" :class="item.icon"></i>{{item.title}}</a></div>
            </div>
            <div class="footer-item">
                <div style="font-size:17px;font-weight: bold;">资源</div>
                <div><a target="_blank" class="out-link" href="#">每周精选</a></div>
                <div><a target="_blank" class="out-link" href="#">简明教程</a></div>
                <div><a target="_blank" class="out-link" href="/">阎世千的官方网站</a></div>
            </div>
            <div class="footer-item">
                <div>本站已苟活 {{runTimeInterval}}</div>
                <div><a target="_blank" class="out-link" href="http://39.107.116.140:100">☞后台管理</a></div>
            </div>
        </div>
        <div class="copyright">Copyright © 2020 by <a target="_blank" class="out-link" href="https://www.ysq.cn">ysq.cn</a> . All rights reserved. | <a target="_blank" class="out-link" href="http://www.beian.miit.gov.cn">渝ICP备17015355号-1</a></div>
    </div>
</template>

<script>
    import sectionTitle from '@/components/section-title'
    import {fetchSocial,fetchBanner} from "../../api";

    export default {
        name: "layout-footer",
        data(){
            return{
                socials: []
            }
        },
        components:{
            sectionTitle
        },
        computed:{
            runTimeInterval() {
                return this.$store.state.runTimeInterval;
            }
        },
        methods:{
            getSocial(){
               fetchSocial().then(response=>{
                 this.socials=response.data.data
               })

            },
        },
        created(){
            this.getSocial();
            this.$store.dispatch('initComputeTime');
        }
    }
</script>

<style scoped lang="less">
#layout-footer{
    padding: 2%;
    border-top: 1px solid #F7F7F7;
    font-size: 13px;
    color: black;
    a.out-link:hover{
        color: #ff6d6d;
    }
    .footer-main{
        max-width: 800px;
        margin: 0 auto 20px auto;
        display: flex;
        justify-content: space-around;
        align-items: flex-start;
        .footer-item{
            flex: 1;
            & > div:not(:last-child){
                margin-bottom: 10px;
            }
            i{
                margin-right: 10px;
            }
        }
    }
    .copyright{
        text-align: center;
    }
}
    /*****/
    @media (max-width: 800px){
        #layout-footer{
            .footer-main .footer-item:nth-child(3){
                flex: 2;
            }
        }
    }
    @media (max-width: 600px){
        #layout-footer{
            .footer-main {
                display: block;
                .footer-item{
                    display: flex;
                    justify-content: space-around;
                    align-items: center;
                    flex-wrap: wrap;
                    & > div{
                        margin-bottom: 10px;
                    }
                }
            }
        }
    }
   .home{
  width: 100%;
  height: 100%;
  background: url("https://edu-yanshiqian.oss-cn-beijing.aliyuncs.com/YxaLMq.jpg") 50% 70% no-repeat;
  //background-size: 100% 100%;
 }
    /*****/
</style>
