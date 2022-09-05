<template>
  <div v-if="!dwhSettings.length">
    <p>First of all it is necessary to fill Database settings</p>
    <a-button type="primary" @click="addConnection">Add Database Connection</a-button>
  </div>
  <a-tabs v-else v-model:activeKey="activeKey" type="editable-card">
    <a-tab-pane key="1" class="content-tab-holder" v-for="(connection, index) in dwhSettings">
      <template #tab>
        <span v-if="!connection.connectionName">
          <a-input-group compact style="width: 60%">
            <a-input placeholder="DB Name" v-model:value="connection.newConnectionName" autofocus autoSize />
            <a-button type="primary" @click="saveConnectionName(index)">Save</a-button>
          </a-input-group>
        </span>
        <span v-else>{{ connection.connectionName }}</span>
      </template>

      <dwhSettingsForm :formState="connection" />
    </a-tab-pane>
  </a-tabs>
</template>
<script lang="ts">
import {defineComponent, ref, reactive} from 'vue';
import dwhSettingsForm from './dwhSettingsForm.vue';

export default defineComponent({
  components: {
    dwhSettingsForm,
  },
  setup() {
    // const dwhSettings = reactive([
    //   {
    //     connectionId: "1",
    //     connectionName: "",
    //     host: "localhost",
    //     port: "5432",
    //     username: "postgres",
    //     password: "postgres",
    //     database: "postgres",
    //     ssl: true,
    //   },
    // ]);
    const dwhSettings = reactive([]);

    const addConnection = () => {
      dwhSettings.push({
        editMode: true,
      });
    }

    const saveConnectionName = (index) => {
      dwhSettings[index].connectionName = dwhSettings[index].newConnectionName;
    };

    return {
      addConnection,
      saveConnectionName,
      dwhSettings,
      activeKey: ref('1'),
    };
  },
});
</script>

<style lang="css" scoped>
.content-tab-holder {
  border: 1px solid #f0f0f0;
  border-top: 0;
  margin-top: -16px;
  padding-top: 16px;
}
</style>
