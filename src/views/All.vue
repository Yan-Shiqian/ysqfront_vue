<template>
  <div class="home">
    <banner isHome="false" :src="banner.imageUrl"></banner>
    <div class="site-content animate">
      <!--通知栏-->
      <div class="notify">
        <div class="search-result">
          <span>全部文章</span>
        </div>
      </div>
      <span class="demonstration"></span>
    </div>
    <div class="site-content animate">
      <!--文章列表-->
      <main  class="site-main">
        <template v-for="item in list">
          <post :post="item" :key="item.id"></post> <!--父子组件？-->
        </template>
      </main>
          <el-pagination
              :current-page="page"
              :page-size="limit"
              :total="total"
              style="padding: 30px 0; text-align: center;"
              layout="total, prev, pager, next, jumper"
              @current-change="fetchList"
          />

    </div>
  </div>
</template>

<script>
import Banner from '@/components/banner'
import Feature from '@/components/feature'
import sectionTitle from '@/components/section-title'
import Post from '@/components/post'
import SmallIco from '@/components/small-ico'
import Quote from '@/components/quote'
import HeaderSearch from '@/components/header-search'
import {fetchBanner, fetchList} from '../api'
export default {
  name: 'Home',
  props: ['cate', 'words'],
  data() {
    return {
      list:null,//查询之后接口返回集合
      page:1,//当前页
      limit:5,//每页记录数
      total:0,//总记录数
      blogQuery:{},//条件封装对象
      description: '',
      classData: null,
      show:false,
      cat:'',
      banner:{}
    }
  },
  components: {
    Banner,
    Feature,
    sectionTitle,
    Post,
    SmallIco,
    Quote,
    HeaderSearch
  },

  computed: {
    searchWords() {
      return this.$route.params.words
    },
    category() {
      return this.$route.params.cate
    },
    hideSlogan() {
      return this.$route.params.cate || this.searchWords
    },
    notice() {
      return this.description
    }
  },
  watch: {  //监听
    $route(to, from) { //路由变化方式，路由发生变化，方法就会执行
      this.fetchList()
    }
  },
  methods: {
    fetchList(page=1) {
      this.page = page
      fetchList(this.page,this.limit,this.blogQuery).then(response => {
        //response接口返回的数据
        this.list = response.data.rows
        this.total = response.data.total
        console.log(this.list)
        console.log(this.total)
      }).catch(err => {
        console.log(err)
      })
    },
    getBanner(){
      fetchBanner().then(response=>{
        this.banner = response.data.data
      })
    },

  },
  mounted() {
    this.fetchList()
    this.getBanner()
  }

}
</script>
<style scoped lang="less">

.site-content {
  .notify {
    margin: 60px 0;
    border-radius: 3px;
    & > div {
      padding: 20px;
    }
  }


  .search-result {
    padding: 15px 20px;
    text-align: center;
    font-size: 20px;
    font-weight: 400;
    border: 1px dashed #ddd;
    color: #828282;
  }
}

.top-feature {
  width: 100%;
  height: auto;
  margin-top: 30px;

  .feature-content {
    margin-top: 10px;
    display: flex;
    justify-content: space-between;
    position: relative;

    .feature-item {
      width: 32.9%;
    }
  }
}

.site-main {
  padding-top: 80px;

  &.search {
    padding-top: 0;
  }
}

.more{
  margin: 50px 0;
  .more-btn{
    width: 100px;
    height: 40px;
    line-height: 40px;
    text-align: center;
    color: #ADADAD;
    border: 1px solid #ADADAD;
    border-radius: 20px;
    margin: 0 auto;
    cursor: pointer;
    &:hover{
      color: #8fd0cc;
      border: 1px dashed #8fd0cc;
    }
  }
}

/******/
@media (max-width: 800px) {
  .top-feature {
    display: none;
  }

  .site-main {
    padding-top: 40px;
  }

  .site-content {
    .notify {
      margin: 30px 0 0 0;
    }

    .search-result {
      margin-bottom: 20px;
      font-size: 16px;
    }
  }
}

/******/
</style>
