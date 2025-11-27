<template>
  <div class="ui container">
    <div class="ui secondary pointing menu massive blue custom-menu">
      <router-link to="/words" class="item" active-class="active">
        <i class="home icon"></i> Home
      </router-link>
      <router-link to="/words/new" class="item" active-class="active">
        <i class="plus circle icon"></i> Add Word
      </router-link>
      <router-link to="/test" class="item" active-class="active">
        <i class="check circle icon"></i> Test
      </router-link>
      
      <div class="right menu">
        <div class="item">
          <div class="ui icon input transparent-input">
            <input 
              type="text" 
              placeholder="Search vocabulary..." 
              v-model="keyword"
              @keyup.enter="onSearch"
            >
            <i class="search link icon" @click="onSearch"></i>
          </div>
        </div>
      </div>
    </div>

    <div class="ui segment main-content">
      <router-view :key="$route.fullPath" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      keyword: ''
    };
  },
  methods: {
    onSearch() {
      // Chuyển hướng sang trang danh sách với tham số tìm kiếm
      this.$router.push({ name: 'words', query: { q: this.keyword } });
    }
  }
};
</script>

<style>
.ui.container {
  margin-top: 30px;
  max-width: 950px !important;
}
.ui.secondary.pointing.menu .item.active {
  border-color: #2185d0 !important;
  color: #2185d0 !important;
  font-weight: bold;
}
.ui.secondary.pointing.menu .item:hover {
  color: #0d47a1 !important;
}
.main-content {
  background: white !important;
  min-height: 500px;
}
</style>