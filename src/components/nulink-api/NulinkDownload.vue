<template>
  <div style="display: flex">
    <div class="box">
      <div class="title-span">
        <span class="title">Description:</span>
        <span>The fileDownload API provides the function of downloading files.</span>
      </div>
      <div class="option">
        <div class="option-title">Option:</div>
        <div class="input-fileId">
          <a-row>
            <a-col :span="4" style="display: flex;align-items: center">FileName:</a-col>
            <a-col :span="10"><a-input v-model:value="fileName" placeholder="guo.jpeg" style="width: 400px"/></a-col>
          </a-row>
        </div>
        <div class="input-fileId">
          <a-row>
            <a-col :span="4" style="display: flex;align-items: center">FileId:</a-col>
            <a-col :span="10"><a-input v-model:value="fileId" placeholder="CyGLEdDXEhuYx_RsS5EFW" style="width: 400px"/></a-col>
          </a-row>
        </div>
        <div class="input-fileId">
          <a-row>
            <a-col :span="4" style="display: flex;align-items: center">UserAddress:</a-col>
            <a-col :span="10"><a-input v-model:value="applyUserAddress" placeholder="0x335de3c07c482f401a82099653977744fb49f075" style="width: 400px"/></a-col>
          </a-row>
        </div>
        <button class="upload" @click="nuLinkDownload">Download</button>
      </div>
      <div class="response" v-if="responseShow">
        <p class="res-title">Response:</p>
        <div>
          <JsonViewer :value="downloadData" sort theme="dark" class="json-viewer-container"/>
        </div>
      </div>
    </div>
    <div class="box">
      <div class="code-style">Code:</div>
      <div>
        <pre v-highlightjs><code class="javascript">{{ downloadCode }}</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import {ref} from "vue";
import {JsonViewer} from "vue3-json-viewer"
import { download }  from "@nulink_network/nulink-web-agent-access-sdk"
import {message} from "ant-design-vue";
const responseShow = ref(false)
const fileName = ref('')
const fileId = ref('')
const applyUserAddress = ref('')

const downloadData = ref()
const downloadCode = 'import { download }  from "@nulink_network/nulink-web-agent-access-sdk"\n' +
    '\n' +
    'const fileDownload = async () => {\n' +
    '    await download(fileId,fileName, applyUserAddress,async (responseData) => {\n' +
    '        if (responseData) {\n' +
    '            // Do something with the responseData\n' +
    '            console.log(responseData)\n' +
    '        } else {\n' +
    '            console.error(\'Failed to upload\');\n' +
    '        }\n' +
    '    });\n' +
    '};'

const nuLinkDownload = async () => {
  await download(fileId.value,fileName.value, applyUserAddress.value,async (responseData) => {
    console.log(responseData);
    if (responseData) {
      // Do something with the responseData
      responseShow.value = true
      downloadData.value = responseData
    } else {
      message.error("Failed to connect agent")
      console.error('Failed to login in');
    }
  });
}



</script>

<style scoped lang="less">
.box {
  flex: 1;
  padding: 0 8px;
}
.upload {
  cursor: pointer;
  color: #fff;
  font-weight: 400;
  font-size: 14px;
  background: #df9100;
  border-radius: 20px;
  height: 24px;
  width: 80px;
  outline: none;
  border: 0px solid transparent;
}
.input-fileId {
  margin-bottom: 8px;
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