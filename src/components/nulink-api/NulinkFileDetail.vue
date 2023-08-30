<template>
  <div style="display: flex">
    <div class="box">
      <div class="title-span">
        <span class="title">Description:</span>
        <span>Get file details.</span>
      </div>
      <div class="option">
        <div class="option-title">Option:</div>
        <div class="input-fileId">
          <a-row>
            <a-col :span="4" style="display: flex;align-items: center">FileId:</a-col>
            <a-col :span="10"><a-input v-model:value="fileId" placeholder="9twES4kp5q9acz00OYaoo" style="width: 550px"/></a-col>
          </a-row>
        </div>
        <div class="input-fileId">
          <a-row>
            <a-col :span="4" style="display: flex;align-items: center">FileAccountId:</a-col>
            <a-col :span="10"><a-input v-model:value="fileUserAccountId" style="width: 550px" placeholder="972ed25f1551dac23a0abfa14f8ea4497a4b6d9b641c6bc93316d846a34332d7" /></a-col>
          </a-row>
        </div>
        <button class="upload" @click="nuLinkFileDetail">GetFileDetail</button>
      </div>
      <div class="response" v-if="responseShow">
        <p class="res-title">Response:</p>
        <div>
          <JsonViewer :value="fileDetailData" sort theme="dark" class="json-viewer-container"/>
        </div>
      </div>
    </div>
    <div class="box">
      <div class="code-style">Code:</div>
      <div>
        <pre v-highlightjs><code class="javascript">{{ fileDetailCode }}</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import {ref} from "vue";
import {JsonViewer} from "vue3-json-viewer"
import { getFileDetail } from "@nulink_network/nulink-web-agent-access-sdk"


const responseShow = ref(false)
const fileDetailData = ref()
const fileId = ref('')
const fileUserAccountId = ref('')
const fileDetailCode = 'import { getFileDetail }  from "@nulink_network/nulink-web-agent-access-sdk"\n' +
    '\n' +
    '// Parameters\n' +
    '// fileId : string - the file id\n' +
    '// fileUserAccountId : string - The file user\'s account ID\'\n' +
    '\n' +
    'const _getFileDetail = async () => {\n' +
    '    let result = await getFileDetail(\n' +
    '        fileId, fileUserAccountId\n' +
    '    );\n' +
    '    console.log(result)\n' +
    '};'

const nuLinkFileDetail = async () => {
  console.log(fileId.value);
  let result = await getFileDetail(
      fileId.value, fileUserAccountId.value
  );
  responseShow.value = true
  fileDetailData.value = result
}

</script>

<style scoped lang="less">
.box {
  flex: 1;
  padding: 0 8px;
}
.title {
  font-size: 14px;
  font-weight: 800;
  margin-right: 4px;
}
.option-title {
  font-size: 14px;
  font-weight: 800;
  margin-bottom: 8px;
}
.title-span {
  margin-bottom: 8px;
}
.upload {
  cursor: pointer;
  color: #fff;
  font-weight: 400;
  font-size: 14px;
  background: #df9100;
  border-radius: 20px;
  height: 24px;
  width: 95px;
  outline: none;
  border: 0px solid transparent;
}
.input-fileId {
  margin-bottom: 8px;
}
.code-style {
  font-size: 14px;
  font-weight: 800;
  margin-bottom: 8px;
}
.res-title {
  font-size: 14px;
  font-weight: 800;
  margin-top: 8px;
}
.json-viewer-container {
  max-height: 300px;
  overflow-y: auto;
}
</style>