<template>
  <div
    class="header"
    style="position:fixed;top:0;left:0;width:100%;z-index:999"
  >
    <a-row type="flex" justify="center">
      <a-col :xs="21" :sm="21" :md="11" :lg="16" :xl="15" >
        <span class="header-logo" @click="handleClickHome" style="cursor: pointer">Neekko33's</span>
        <span class="header-txt">Blog</span>
      </a-col>
      <a-col
        class="memu-div"
        :xs="3"
        :sm="3"
        :md="13"
        :lg="7"
        :xl="4"
        style="text-align:right"
      >
      </a-col>
    </a-row>
  </div>
</template>

<script>

export default {
  name: 'Header',
  methods: {
    handleClickHome() {
      this.$router.push('/')
    },
  }
}
</script>

<style scoped>
.header {
  background-color: #fff;
  padding: 0.4rem;
  overflow: hidden;
  height: 3.2rem;
  border-bottom: 1px solid #eee;
  box-shadow: 0px 1px 3px 0px rgba(0, 0, 0, 0.1);
}

.header-logo {
  color: #1e90ff;
  font-size: 1.4rem;
  text-align: left;
}

.header-txt {
  font-size: 0.6rem;
  color: #999;
  display: inline-block;
  padding-left: 0.3rem;
}

.ant-menu {
  line-height: 2.8rem;
}

.ant-menu-submenu {
  line-height: 2.8rem;
}

.ant-menu-item {
  font-size: 1rem !important;
  padding: 0px !important;
  text-align: center;
}

.submenu-title-wrapper {
  font-size: 1rem !important;
  padding-left: 1rem;
  padding-right: 1rem;
}
</style>
