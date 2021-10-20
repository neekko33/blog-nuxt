<template>
  <div class='container'>
    <div class='tags_title'>
      最近文章
    </div>
    <div class='article_list'>
      <div class='article_item' v-for='item in articleList' :key='item.id'>
        <nuxt-link :to="'/detailed?id=' + item.id">
          <div class='article_time'>{{formatTime(item.addTime)}}</div>
          <div class='article_title'>{{item.title}}</div>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment'
import _ from 'lodash'

export default {
  name: 'News',
  props: {
    list: Array,
  },
  data() {
    return {
      articleList:[],
    }
  },
  created() {
    this.articleList = _.cloneDeep(this.list).splice(0,4);
  },
  methods:{
    formatTime(time) {
      return moment(Number(time)).format('YYYY-MM-DD')
    },
  }
}
</script>

<style scoped>
.container {
  padding: 1rem;
}

.tags_title {
  color: #6b7f94;
  font-size: .9em;
  letter-spacing: 1px;
  margin-bottom: .75rem;
}

.article_item:first-child {
  border: none !important;
}

.article_item {
  padding: .5rem;
  font-size: .85rem;
  line-height: 2;
  margin-bottom: 0;
  text-decoration: none;
  border-top:1px solid #e6e8ee;
}

.article_item a {
  color: #475b6d;
}

.article_item a:hover {
  color: rgba(0, 0, 0, 0.85);
}

</style>
