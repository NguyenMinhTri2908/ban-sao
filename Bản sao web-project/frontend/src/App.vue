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
            <input type="text" placeholder="Search vocabulary...">
            <i class="search link icon"></i>
          </div>
        </div>
      </div>
    </div>

    <div class="ui segment main-content">
      <router-view />
    </div>
  </div>
</template>

<script>
export default {
  name: 'App'
};
</script>

<style>
/* Căn chỉnh lề trên để menu không dính sát mép màn hình */
.ui.container {
  margin-top: 30px;
  max-width: 950px !important; /* Giới hạn chiều rộng tối đa cho đẹp */
}

/* Tăng cường màu sắc cho Menu khi active */
.ui.secondary.pointing.menu .item.active {
  border-color: #2185d0 !important;
  color: #2185d0 !important;
  font-weight: bold;
}

.ui.secondary.pointing.menu .item:hover {
  color: #0d47a1 !important;
}

/* Vùng nội dung chính màu trắng */
.main-content {
  background: white !important;
  min-height: 500px;
}
</style>