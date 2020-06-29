<template>
  <div id="app">
    <el-input v-model="input" disabled placeholder="请输入"></el-input>
  </div>
</template>

<script>
import ElInput from './components/ElInput';

export default {
  name: 'App',
  components: {
    ElInput
  },
  data() {
    return {
      input: '12'
    };
  }
};
</script>

<style></style>
