<template>
  <div class='container' style='padding-top:3.2rem;'>
    <Header />
    <a-row class='comm-main' type='flex' justify='center'>
      <a-col :xs='0' :sm='0' :md='6' :lg='6' :xl='5'>
        <div class='comm-box'>
          <Author-Info />
        </div>
        <div class='comm-box'>
          <Tags />
        </div>
        <div class="comm-box">
          <Archive />
        </div>
      </a-col>
      <a-col :xs='24' :sm='24' :md='12' :lg='12' :xl='9'>
        <div class='comm-left'>
          <Article :list='articleList' :title="'全部文章'" />
        </div>
        <div class='pagination'>
          <a-pagination v-model='current' :total='total' :page-size='pageSize' @change='handleChange' :hideOnSinglePage='true'/>
        </div>
      </a-col>
      <a-col :xs='0' :sm='0' :md='6' :lg='6' :xl='5'>
        <div class='comm-box' style='margin-right: 0;margin-left:1.5rem'>
          <News :list='articleList' />
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
import News from '../components/News'
import { getArticle, getArticleById } from '../api/api'

export default {
  async asyncData() {
    const articleList = await getArticle(1, 7)
    return {
      data: articleList.data.data
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
    Archive,
    News
  },
  head() {
    return {
      title: 'Neekko33\'s Blog'
    }
  },
  data() {
    return {
      articleList: [],
      current: 1,
      total: 0,
      pageSize: 7
    }
  },
  created() {
    this.articleList = _.cloneDeep(this.data.articles)
    this.total = this.data.count
  },
  methods:{
    async handleChange(num) {
      const { data:{ data } } = await getArticle(num,this.pageSize)
      this.articleList = data.articles
      this.current = num
      this.backToTop('title')
    },
    backToTop(anchorName) {
      if (anchorName) {
        let anchorElement = document.getElementById(anchorName)
        if (anchorElement) {
          anchorElement.scrollIntoView(false)
        }
      }
    }
  }
}
</script>

<style src='../styles/comm.css'></style>
