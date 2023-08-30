<template>
  <div style="display: flex">
    <div class="box">
      <div class="title-span">
        <span class="title">Description:</span>
        <span>The apply function is used for applying for files, takes four parameters: fileCreatorAddress,fileId,fileName,usageDays and callBackFunc, which is the callback function to be executed after the application is successful.</span>
      </div>
      <div class="option">
        <div class="option-title">Option:</div>
        <div class="input-fileId">
          <a-row>
            <a-col :span="4" style="display: flex;align-items: center">FileName:</a-col>
            <a-col :span="10"> <a-input v-model:value="fileName" placeholder="3 (9).png" style="width: 400px"/></a-col>
          </a-row>
        </div>
        <div class="input-fileId">
          <a-row>
            <a-col :span="4" style="display: flex;align-items: center">FileId:</a-col>
            <a-col :span="10"><a-input v-model:value="fileId" placeholder="qTZUQB4NgukYa9dvErMuZ" style="width: 400px"/></a-col>
          </a-row>
        </div>
        <div class="input-fileId">
          <a-row>
            <a-col :span="4" style="display: flex;align-items: center">FileCreator:</a-col>
            <a-col :span="10"><a-input v-model:value="fileCreatorAddress" placeholder="0x4f8ea4497a4b6d9b641c6bc93316d846a34332d7" style="width: 400px"/></a-col>
          </a-row>
        </div>
        <div class="input-fileId">
          <a-row>
            <a-col :span="4" style="display: flex;align-items: center">UsageDays:</a-col>
            <a-col :span="10"><a-input v-model:value="usageDays" placeholder="1" style="width: 400px" /></a-col>
          </a-row>
        </div>
        <button class="upload" @click="nuLinkApply">Apply</button>
      </div>
      <div class="response" v-if="responseShow">
        <p class="res-title">Response:</p>
        <div>
          <JsonViewer :value="applyData" sort theme="dark" class="json-viewer-container"/>
        </div>
      </div>
    </div>
    <div class="box">
      <div class="code-style">Code:</div>
      <div>
        <pre v-highlightjs><code class="javascript">{{ applyCode }}</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import {reactive, ref} from "vue";
import {JsonViewer} from "vue3-json-viewer"
import { apply } from "@nulink_network/nulink-web-agent-access-sdk"
import {message} from "ant-design-vue";
const applyFileInfo = reactive({
  fileName:"",
  fileId:"",
  fileCreatorAddress:"",
  usageDays: 0
})
const responseShow = ref(false)
const fileName = ref('')
const fileId = ref('')
const fileCreatorAddress = ref('')
const usageDays = ref()

const applyData = ref()
const applyCode = 'import { approve } from "@nulink_network/nulink-web-agent-access-sdk"\n' +
    '\n' +
    '// Parameters\n' +
    '// applyId : string - the application ID\n' +
    '// applyUserId : string - the application user id\n' +
    '// applyUserAddress : string - the application user address\n' +
    '// days : string - the application days\n' +
    '// remark : string - the remark\n' +
    '// Promise : CallBackFunc - A callback function\n' +
    '    \n' +
    'const approveSubmit = async () => {\n' +
    '    const applyInfo = {\n' +
    '        fileName: "string",\n' +
    '        fileId: "fileId",\n' +
    '        fileCreatorAddress: "string",\n' +
    '        usageDays: 0\n' +
    '    }\n' +
    '    await apply(applyInfo, async (responseData) => {\n' +
    '        if (responseData) {\n' +
    '            // Do something with the responseData\n' +
    '            console.log(responseData);\n' +
    '        } else {\n' +
    '            // Handle the error case\n' +
    '            console.error(\'Failed to apply\');\n' +
    '        }\n' +
    '    });\n' +
    '};'

const nuLinkApply = async () => {
  applyFileInfo.fileId = fileId.value
  applyFileInfo.fileName = fileName.value
  applyFileInfo.fileCreatorAddress = fileCreatorAddress.value
  applyFileInfo.usageDays = usageDays.value
  await apply(applyFileInfo, async (responseData) => {
    if (responseData) {
      // Do something with the responseData
      responseShow.value = true
      applyData.value = responseData
    } else {
      message.error("Apply failed")
      // Handle the error case
      console.error('Apply failed');
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
  width: 72px;
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