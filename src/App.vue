<template>
  <div id="app">
    <el-radio-group v-model="location.isCollapse" @change="tagger" style="margin-bottom: 20px;">
      <el-radio-button :label="false">展开</el-radio-button>
      <el-radio-button :label="true">收起</el-radio-button>
    </el-radio-group>
    <el-menu
      :default-active="location.active"
      class="el-menu-vertical-demo"
      @select="handleSelect"
      :collapse="location.isCollapse"
    >
      <el-submenu index="1">
        <template slot="title">
          <i class="el-icon-location"></i>
          <span slot="title">导航一</span>
        </template>
        <el-menu-item-group>
          <span slot="title">分组一</span>
          <el-menu-item index="1-1">选项1</el-menu-item>
          <el-menu-item index="1-2">选项2</el-menu-item>
        </el-menu-item-group>
        <el-menu-item-group title="分组2">
          <el-menu-item index="1-3">选项3</el-menu-item>
        </el-menu-item-group>
        <el-submenu index="1-4">
          <span slot="title">选项4</span>
          <el-menu-item index="1-4-1">选项1</el-menu-item>
        </el-submenu>
      </el-submenu>
      <el-menu-item index="2">
        <i class="el-icon-menu"></i>
        <span slot="title">导航二</span>
      </el-menu-item>
      <el-menu-item index="3">
        <i class="el-icon-setting"></i>
        <span slot="title">导航三</span>
      </el-menu-item>
    </el-menu>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      location: {
        isCollapse: false,
        active: "3"
      }
    };
  },
  created() {
    this.getLocation();
  },
  mounted() {},
  methods: {
    getLocation() {
      let query = sessionStorage.getItem("location");
      query = query ? JSON.parse(query) : "";
      if (query) {
        this.location = query;
      } else {

      }
    },
    tagger(value) {
      this.location.isCollapse = value;
      let locationData = this.location;
      sessionStorage.setItem("location", JSON.stringify(locationData));
    },
    handleSelect(key) {
      this.location.active = key;
      let locationData = this.location;
      sessionStorage.setItem("location", JSON.stringify(locationData));
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 200px;
  min-height: 400px;
}
</style>
