<template>
  <div class='container'>
    <div class='tags_title'>
      归档 (施工中)
    </div>
    <div class='tags_list'>
      <a class='tags_item'>
        <div class='tags_name'>2021</div>
        <div class='tags_count'>30</div>
      </a>
      <a class='tags_item'>
        <div class='tags_name'>2020</div>
        <div class='tags_count'>15</div>
      </a>
      <a class='tags_item'>
        <div class='tags_name'>2019</div>
        <div class='tags_count'>7</div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'tags'
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
