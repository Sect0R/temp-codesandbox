<template>
  <a-layout>
    <a-layout-sider>Sider</a-layout-sider>
    <a-layout>
      <a-layout-header>Header</a-layout-header>
      <a-layout-content class="app-content">
        <dwhSettings />
      </a-layout-content>
      <a-layout-footer>Footer</a-layout-footer>
    </a-layout>
  </a-layout>
</template>

<script>
import { defineComponent } from "vue";
import dwhSettings from "./views/dwh_settings/dwhSettings.vue";

export default defineComponent({
  components: {
    dwhSettings,
  },
});
</script>

<style lang="css" scoped>
.app-content {
  background-color: #fff;
  padding: 24px;
  border-color: #aaa;
  border-width: 20px;
}
</style>
