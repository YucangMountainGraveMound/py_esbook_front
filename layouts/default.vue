<style scoped>
.layout {
  border: 1px solid #f7f7f7;
  background: #f7f7f7;
  position: relative;
  border-radius: 4px;
  overflow: hidden;
}
.layout-logo {
  width: 100px;
  height: 30px;
  background: #5b6270;
  border-radius: 3px;
  float: left;
  position: relative;
  top: 15px;
  left: 20px;
}
.layout-nav {
  width: 420px;
  margin: 0 auto;
  margin-right: 20px;
}
.layout-footer-center {
  text-align: center;
}
</style>
<template>
  <div class="layout">
    <Layout :style="{background:'#fff'}">
      <Header :style="{position: 'fixed', width: '100%'}">
        <Menu mode="horizontal" theme="dark" active-name="1">
          <div class="layout-logo"></div>
          <div class="layout-nav">
            <MenuItem name="1">
            <Icon type="ios-navigate"></Icon>
            首页
            </MenuItem>
            <MenuItem name="2">
            <div @click="hrefto('/mail')">
              <Icon type="email"></Icon>
              邮箱</div>
            </MenuItem>
            <MenuItem name="3">
            <div @click="hrefto('/book/list')">
              <Icon type="ios-paper"></Icon>
              我的书架</div>
            </MenuItem>
            <Submenu name="4">
              <template slot="title">
                <Icon type="ios-person"></Icon>
                登录
              </template>
              <MenuGroup title="设置">
                <MenuItem name="4-1">
                <div @click="hrefto('/mail')">
                  <Icon type="email"></Icon>
                  新增邮箱
                </div>
                </MenuItem>
                <MenuItem name="4-2">
                <div @click="hrefto('/book/add')">
                  <Icon type="ios-bookmarks"></Icon>
                  新增书籍
                </div>
                </MenuItem>

                <MenuItem name="4-3">
                <Icon type="person"></Icon>
                个人资料</MenuItem>
                <MenuItem name="4-4">
                <Icon type="log-out"></Icon>
                s登出</MenuItem>
              </MenuGroup>
            </Submenu>
          </div>
        </Menu>
      </Header>
      <Content :style="{margin: '0', background: '#f7f6f2', minHeight: '888px',padding:'88px 0 0 0'}">
        <nuxt></nuxt>
      </Content>
      <Footer class="layout-footer-center">2011-2016 &copy; ESBOOK</Footer>
    </Layout>
  </div>
</template>
<script>
export default {
  methods: {
    hrefto(addr) {
      this.$router.push(addr)
    }
  }
}
</script>
