<template>
  <div class='container'>
    <div class='tags_title'>
      分类
    </div>
    <div class='tags_list'>
      <a class='tags_item' v-for='item in typeList' :key='item.id' @click='handleClickType(item.id)'>
        <div class='tags_name'>{{item.typeName}}</div>
        <div class='tags_count'>{{item.articles.length}}</div>
      </a>
    </div>
  </div>
</template>
<script>
import { getType } from '../api/api'

export default {
  name: 'tags',
  data() {
    return {
      typeList: null
    }
  },
  async mounted() {
    const typeList = window.sessionStorage.getItem('type_list')
    if (typeList) {
      this.typeList = JSON.parse(typeList)
    } else {
      const {
        data: { data }
      } = await getType()
      this.typeList = data.filter(item => item.id != 4)
      window.sessionStorage.setItem('type_list', JSON.stringify(this.typeList))
    }
  },
  methods: {
    handleClickType(id) {
      this.$router.push({ name: 'list', query: { id } })
    }
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

.tags_item {
  display: flex;
  justify-content: space-between;
  line-height: 1.25;
  color: #37475b;
  padding: .5rem;
}

.tags_item:hover {
  background: #eceef2;
}

.tags_count {
  background: #eceef2;
  border-radius: 4px;
  font-size: .75rem;
  height: 1.5em;
  line-height: 1.5;
  padding: .1em .75em;
}
</style>
