<template>
  <div style='padding-top:3.2rem'>
    <Header />
    <a-row class='comm-main' type='flex' justify='center'>
      <a-col :xs='0' :sm='0' :md='5' :lg='5' :xl='5'>
        <div class='comm-box'>
          <Author-Info />
        </div>
        <div class='comm-box'>
          <Tags />
        </div>
        <div class='comm-box'>
          <Archive />
        </div>
      </a-col>
      <a-col :xs='24' :sm='24' :md='14' :lg='14' :xl='9'>
        <div class='comm-left'>
          <div class='bread-div'>
            <a-breadcrumb>
              <a-breadcrumb-item>
                <a href='/' id='title'>首页</a>
              </a-breadcrumb-item>
              <a-breadcrumb-item>
                {{
                  myList.length > 0 ? myList[0].type.typeName : '暂无文章'
                }}
              </a-breadcrumb-item>
            </a-breadcrumb>
          </div>
          <Article :list='myList' :title="''" :hasBorder='myList.length < 4' />
        </div>
        <div class='pagination'>
          <a-pagination v-model='current' :total='total' :page-size='pageSize' @change='handleChange'
                        :hideOnSinglePage='true' />
        </div>
      </a-col>
      <a-col :xs='0' :sm='0' :md='5' :lg='5' :xl='5'>
        <div class='comm-box' style='margin-right: 0;margin-left:1.5rem'>
          <News :list='articles' />
        </div>
      </a-col>
    </a-row>
    <Footer />
    <ScrollToTop />
  </div>
</template>

<script>
import { getArticle, getArticleById, getArticleByType } from '../../api/api'
import Header from '../../components/Header.vue'
import Footer from '../../components/Footer'
import ScrollToTop from '../../components/ScrollToTop'
import Article from '../../components/Article'
import AuthorInfo from '../../components/AuthorInfo'
import Archive from '../../components/Archive'
import Tags from '../../components/Tags'
import News from '../../components/News'

export default {
  async asyncData({ query }) {
    const articleList = await getArticle(1, 4)
    const {
      data: { data }
    } = await getArticleByType(query.id, 1, 7)
    return {
      myList: data.articles,
      total: data.count,
      articles: articleList.data.data.articles,
      typeId: query.id
    }
  },
  watchQuery: ['id'],
  name: 'index',
  components: {
    Article,
    Header,
    Footer,
    AuthorInfo,
    Archive,
    ScrollToTop,
    Tags,
    News
  },
  head() {
    return {
      title: '文章分类'
    }
  },
  data() {
    return {
      current: 1,
      pageSize: 7
    }
  },
  methods: {
    async handleChange(num) {
      const { data: { data } } = await getArticleByType(this.typeId, num, this.pageSize)
      this.myList = data.articles
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

<style scoped src='../../styles/comm.css'></style>
<style>
.my_list {
  border-bottom: 1px solid #e8e8e8 !important;
}
</style>
