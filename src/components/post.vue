<template>
    <article class="post post-list">
        <div class="post-entry home1">
<!--            <div class="feature">-->
<!--                <router-link :to="`/article/${post.id}`">-->
<!--                    <img src="../assets/1.jpg"/>-->
<!--                </router-link>-->
<!--      每个博客的图片      </div>-->

            <h1 class="entry-title">
                <router-link :to="`/article/${post.id}`">{{post.title}}</router-link>
            </h1>

            <div class="p-time">
                <i class="iconfont iconmeditor-time"></i> {{post.gmtModified | parseTime}}<i v-if="post.isHot" class="iconfont iconfire" style="margin-left: 5px;color: #ff6d6d;"></i>
            </div>

            <p class="summary">{{post.description}} </p>

            <footer class="entry-footer">
                <div class="post-more">
                    <router-link :to="`/article/${post.id}`"><i class="iconfont iconfish-li" style="font-size: 25px;"></i></router-link>
                </div>
                <div class="info-meta">
                    <div class="comnum">
                        <span>
                            <i class="iconfont iconcomment"></i>
                            <a href="https://zhebk.cn/Web/Akina.html">{{post.commentsCount}} 条评论</a>
                        </span>
                    </div>
                    <div class="views">
                        <span><i class="iconfont iconeyes"></i>{{post.sort}} 热度</span>
                    </div>
                </div>
            </footer>
        </div>
<!--        <hr/>-->
    </article>
</template>

<script>

    export default {
        name: "post",
        props: {
            post: {
                type: Object
            }
        }
    }
</script>

<style scoped lang="less">
    .post {
        margin: 0 0 2% 0;
       // float: left;
        position: relative;

    }

    .post-entry {
        .feature {
            position: absolute;
           // margin-top: 10px;

            //
            //img {
            //    width: 100px;
            //    height: 100px;
            //    object-fit: cover;
            //    border-radius: 50%;
            //    padding: 2px;
            //    border: 1px solid #DADADA;
            //    position: relative;
            //    transition: all 0.2s linear;
            //    overflow: hidden;
            //    &:hover {
            //        transform: scale(1.1, 1.1);
            //        filter: contrast(130%);
            //    }
            //}
        }
        .entry-title {
            //float: left;
            font-size: 21px;
            font-weight: 600;
            line-height: 50px;
            margin: 0 0 0 2%;
            position: relative;
            z-index: 1;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            width: 70%;
            color: #737373;
            //color: black;

            & a:hover {
                color: #8fd0cc;
            }
        }

        .p-time {
            //position: absolute;
            margin-right: 20px;
            float: right;
            right: 0;
            top: 16px;
            font-size: 12px;
            color: #989898;
            letter-spacing: 1px;
            font-family: din, 'Hiragino Sans GB', 'Microsoft Yahei', Arial, sans-serif;
            display: flex;
            align-items: center;
        }

        p.summary {
            min-height: 60px;
            margin: 0 0 0 2%;
            font-size: 15px;
            color: #6f6f6f;
            letter-spacing: 1px;
            line-height: 30px;
        }

        footer.entry-footer {
            //margin: 0 0 0 17%;
            margin-right: 20px;
            list-style: none;

            .post-more {
                margin-top: 10px;
                text-align: right;
                color: #A0DAD0;

                a:hover {
                    color: #737373;
                }
            }

            .info-meta {
                margin-top: 10px;
                font-family: din, 'Hiragino Sans GB', 'Microsoft Yahei', Arial, sans-serif;
                position: absolute;
                top: 20px;
                opacity: 0;
                padding-top: 8px;
                border-top: 1px solid #ddd;
                -webkit-transform: translate3d(-150px, 0, 0);
                transform: translate3d(-150px, 0, 0);
                visibility: hidden;
                transition: .7s all ease;
                -webkit-transition: .6s all ease;
                -moz-transition: .6s all linear;
                -o-transition: .6s all ease;
                -ms-transition: .6s all ease;

                span, a {
                    color: #B3B3B3;
                    font-size: 12px;
                }

                i {
                    margin-top: 3px;
                    margin-right: 10px;
                    float: left
                }
            }

            .comnum {
                float: left;
            }
        }

    }

    .post-entry:hover footer.entry-footer .info-meta {
        -webkit-transform: translate3d(-100px, 0, 0);
        transform: translate3d(-100px, 0, 0);
        opacity: 1;
        visibility: visible;
    }

    .post hr {
        width: 60%;
        border: 1px dashed #ddd;
    }

    .home1:hover {
      transition: all 0.2s linear;
      background: #f1f1f1;
    }
    .home1{
      width: 60%;
      height: 60%;
      background: white;
      border-radius: 15px;
      //background-size: 10% 10%;
    }

    /*******/
    @media (max-width: 1060px) {
        .info-meta{
            display: none;
        }
    }
    @media (max-width: 800px) {
          .home1{
            background: unset;
            width: 100%;
          }
          .post-entry {
            //.feature img {
            //    width: 50px;
            //    height: 50px;
            //}

            .entry-title{
                font-size: 16px;
                line-height: 30px;
                margin: 0 0 0 5px;
            }
            .p-time {
                position: relative;
                margin: -15px 0 0 65px;
            }
            p.summary {
                margin: 20px 0 0 5px;
                font-size: 14px;
                height: 30px;
                overflow: hidden;
            }
            .post-more{
                display: none;
            }
            .home1{
              display: none;
            }
        }
        .post-list hr {
            margin-top: 20px;
        }
    }


    /******/
</style>
