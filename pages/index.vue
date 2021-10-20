<template>
  <div class="container" style="padding-top:3.2rem;">
    <Header />
    <a-row class="comm-main" type="flex" justify="center">
      <a-col :xs="0" :sm="0" :md="8" :lg="6" :xl="5">
        <div class='comm-box'>
          <Author-Info />
        </div>
        <div class="comm-box">
          <Tags />
        </div>
        <div class="comm-box">
          <Archive />
        </div>
      </a-col>
      <a-col :xs="24" :sm="24" :md="16" :lg="18" :xl="14">
        <div class="comm-left">
          <Article :list="articleList" :title="'最新文章'" />
        </div>
      </a-col>
    </a-row>
    <Footer />
    <ScrollToTop />
  </div>
</template>

<script>
import _ from 'lodash'
import Header from '../components/Header.vue'
import Article from '../components/Article'
import Footer from '../components/Footer'
import AuthorInfo from '../components/AuthorInfo'
import ScrollToTop from '../components/ScrollToTop'
import Tags from '../components/Tags'
import Archive from '../components/Archive'
import { getArticle,getArticleById } from '../api/api'

export default {
  async asyncData() {
    const articleList = await getArticle(1, 10)
    return {
      myList: articleList.data.data.articles,
    }
  },
  name: 'index',
  components: {
    Header,
    Article,
    Footer,
    AuthorInfo,
    ScrollToTop,
    Tags,
    Archive
  },
  head() {
    return {
      title: 'Neekko33\'s Blog'
    }
  },
  data() {
    return {
      articleList: []
    }
  },
  created() {
    const list = _.cloneDeep(this.myList)
    this.articleList = list.filter(item => {
      return item.id != 4
    })
  }
}
</script>

<style src="../styles/comm.css"></style>
