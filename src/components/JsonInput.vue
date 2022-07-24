<template>
  <div class="my-container" style="padding: 0">
    <el-input type="textarea" :rows="2" placeholder="请输入hive query explain" v-model="textarea" @input="sendJsonStr">
    </el-input>
  </div>

</template>

<script>
import eventBus from "../eventBus/event-bus";

export default {
  name: "JsonInput",
  data() {
    return {
      textarea: ''
    }
  },
  methods: {
    sendJsonStr: function () {
      eventBus.$emit('textChange', JSON.parse(this.textarea));
    }
  }
}
</script>

<style scoped>

</style>