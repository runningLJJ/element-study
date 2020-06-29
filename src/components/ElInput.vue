<template>
  <div :class="[type === 'textarea' ? 'el-textarea' : 'el-input', { 'is-disabled': inputDisabled }]">
    <template v-if="type !== 'textarea'">
      <input
        :type="type"
        class="el-input__inner"
        :disabled="disabled"
        v-bind="$attrs"
        ref="input"
        @input="handleInput"
        @blur="handleBlur"
        @focus="handleFocus"
        @change="handleChange"
      />
    </template>
    <textarea v-else></textarea>
  </div>
</template>

<script>
export default {
  name: 'ElInput',
  inheritAttrs: false,
  props: {
    value: [String, Number],
    type: {
      type: String,
      default: 'text'
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {};
  },
  computed: {
    /**
     * 从父组件el-input的v-model传下来的原生value值，监听变化，修改input的value值
     */
    nativeInputValue() {
      return this.value === null || this.value === undefined ? '' : String(this.value);
    },
    inputDisabled() {
      return this.disabled;
    }
  },
  watch: {
    nativeInputValue() {
      this.setNativeInputValue();
    }
  },
  mounted() {
    this.setNativeInputValue();
  },
  methods: {
    setNativeInputValue() {
      const input = this.getInput();
      if (!input) return;
      if (input.value === this.nativeInputValue) return;
      input.value = this.nativeInputValue;
    },
    getInput() {
      return this.$refs.input || this.$refs.textarea;
    },
    handleInput(event) {
      this.$emit('input', event.target.value);
    },
    handleBlur() {},
    handleFocus() {},
    handleChange(event) {
      this.$emit('change', event.target.value);
    }
  }
};
</script>

<style>
.el-input {
  position: relative;
  display: inline-block;
  font-size: 14px;
  width: 180px;
}
.el-input__inner {
  width: 100%;
  background-color: #fff;
  border-radius: 4px;
  border: 1px solid #dcdfe6;
  box-sizing: border-box;
  display: inline-block;
  color: #606626;
  height: 40px;
  line-height: 40px;
  outline: none;
  padding: 0 15px;
  cursor: pointer;
  transition: border-color 0.2s;
}
.el-input__inner:hover {
  border-color: #c0c4cc;
}
.el-input__inner:focus {
  border-color: #409eff;
  outline: none;
}
.el-input__inner::placeholder {
  color: #c0c4cc;
}
.el-input.is-disabled .el-input__inner {
  cursor: not-allowed;
  background-color: #f5f7fa;
  color: #c0c4cc;
  border-color: #e4e7ed;
}
</style>
