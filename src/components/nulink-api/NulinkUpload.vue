<template>
  <div style="display: flex;">
    <div class="box">
      <div class="title-span">
        <span class="title">Description:</span>
        <span>Upload used for uploading files and executing a callback function after the upload is successful</span>
      </div>
      <div class="option">
        <span class="option-title">Option:</span>
        <button class="upload" @click="nuLinkUpload">Upload</button>
      </div>
      <div class="response" v-if="responseShow">
        <p class="res-title">Response:</p>
        <div>
          <JsonViewer :value="uploadData" sort theme="dark" class="json-viewer-container"/>
        </div>
      </div>
    </div>
    <div class="box">
      <div class="code-style">Code:</div>
      <div>
        <pre v-highlightjs><code class="javascript">{{ uploadCode }}</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import {ref} from "vue";
import {JsonViewer} from "vue3-json-viewer"
import { upload } from "@nulink_network/nulink-web-agent-access-sdk"
import {message} from "ant-design-vue";

const responseShow = ref(false)
const uploadData = ref()
const uploadCode = 'import { upload } from "@nulink_network/nulink-web-agent-access-sdk"\n' +
    '\n' +
    'const gotoUpload = async () => {\n' +
    '    await upload(uploadSuccessHandler)\n' +
    '}\n' +
    '\n' +
    'const uploadSuccessHandler = async (responseData) => {\n' +
    '    if (responseData) {\n' +
    '        // Do something with the responseData\n' +
    '        console.log(responseData);\n' +
    '    } else {\n' +
    '        // Handle the error case\n' +
    '        console.error(\'Upload failed\');\n' +
    '    }\n' +
    '}'

const nuLinkUpload = async () => {
  await upload(uploadSuccessHandler)
}

const uploadSuccessHandler = async (responseData) => {
  if (responseData) {
    // Do something with the responseData
    responseShow.value = true
    uploadData.value = responseData
  } else {
    // Handle the error case
    message.error("Upload failed")
    console.error('Failed to login in');
  }
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
.title-span {
  margin-bottom: 8px;
}

.option-title {
  font-size: 14px;
  font-weight: 800;
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
  width: 72px;
  outline: none;
  border: 0px solid transparent;
  margin-left: 8px;
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