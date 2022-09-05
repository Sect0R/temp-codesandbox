<template>
  <a-form
    :model="formState"
    name="basic"
    :label-col="{ span: 2 }"
    :wrapper-col="{ span: 12 }"
    autocomplete="off"
    @finish="onFinish"
    @finishFailed="onFinishFailed"
  >

    <div class="pos-absolute ant-col-offset-14">
      <a-button type="primary" size="large" :disabled="formState.editMode" @click="edit"> Edit</a-button>
      <a-button type="danger" size="large" style="margin-left: 10px"> Delete</a-button>
    </div>

    <a-form-item
      label="Host"
      name="host"
      :rules="[{ required: true, message: 'Please input host!' }]"
    >
      <a-input v-model:value="formState.host" :disabled="!formState.editMode" />
    </a-form-item>

    <a-form-item
      label="Port"
      name="port"
      :rules="[{ required: true, message: 'Please input port!' }]"
    >
      <a-input-number v-model:value="formState.port" :disabled="!formState.editMode" />
    </a-form-item>

    <a-form-item
      label="Username"
      name="username"
      :rules="[{ required: true, message: 'Please input username!' }]"
    >
      <a-input v-model:value="formState.username" :disabled="!formState.editMode" />
    </a-form-item>

    <a-form-item
      label="Password"
      name="password"
      :rules="[{ required: true, message: 'Please input password!' }]"
    >
      <a-input-password v-model:value="formState.password" :disabled="!formState.editMode" />
    </a-form-item>

    <a-form-item
      label="Database"
      name="database"
      :rules="[{ required: true, message: 'Please input database!' }]"
    >
      <a-input v-model:value="formState.database" :disabled="!formState.editMode" />
    </a-form-item>

    <a-form-item name="ssl" :wrapper-col="{ offset: 2 }">
      <a-checkbox v-model:checked="formState.ssl" :disabled="!formState.editMode">use SSL</a-checkbox>
    </a-form-item>

    <a-form-item :wrapper-col="{ offset: 16 }">
      <a-button type="primary" html-type="submit" :disabled="!formState.editMode" @click="save">
        Connect
      </a-button>
    </a-form-item>
  </a-form>
</template>

<script lang="ts">
import { defineComponent, ref, reactive } from 'vue';

export default defineComponent({
  setup(props) {
    const formState = reactive(props.formState);

    const onFinish = values => {
      console.log('Success:', values);
    };

    const onFinishFailed = errorInfo => {
      console.log('Failed:', errorInfo);
    };

    const save = () => {
      formState.editMode = false;
    };

    const edit = () => {
      formState.editMode = true;
    };

    return {
      activeKey: ref('1'),
      formState,
      save,
      edit,
      onFinish,
      onFinishFailed,
    };
  },
  props: {
    formState: Object,
  },
});
</script>

<style lang="css" scoped>
.pos-absolute {
  position: absolute;
}
</style>
