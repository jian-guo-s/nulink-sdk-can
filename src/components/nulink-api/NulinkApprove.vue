<template>
  <div style="display: flex">
    <div class="box">
      <div class="title-span">
        <span class="title">Description:</span>
        <span>Approveis used for approving files, takes six parameters: applyId, applyUserId, applyUserAddress, days, remark, and callBackFunc.</span>
      </div>
      <div class="option">
        <div class="option-title">Option:</div>
        <div class="input-fileId">
          <a-row>
            <a-col :span="4" style="display: flex;align-items: center">ApplyId:</a-col>
            <a-col :span="10"> <a-input v-model:value="applyId" placeholder="5212" style="width: 400px"/></a-col>
          </a-row>
        </div>
        <div class="input-fileId">
          <a-row>
            <a-col :span="4" style="display: flex;align-items: center">ApplyUserId:</a-col>
            <a-col :span="10"><a-input v-model:value="applyUserId" placeholder="69c3c363d41ea460aa59439a836c35165d3d721264845f7cc1b6927fee8eef82" style="width: 400px"/></a-col>
          </a-row>
        </div>
        <div class="input-fileId">
          <a-row>
            <a-col :span="4" style="display: flex;align-items: center">UserAddress:</a-col>
              <a-col :span="10"><a-input v-model:value="applyUserAddress" placeholder="0x836c35165d3d721264845f7cc1b6927fee8eef82" style="width: 400px"/></a-col>
          </a-row>
        </div>
        <div class="input-fileId">
          <a-row>
            <a-col :span="4" style="display: flex;align-items: center">Days:</a-col>
            <a-col :span="10"><a-input v-model:value="days" placeholder="1" style="width: 400px" /></a-col>
          </a-row>
        </div>
        <button class="upload" @click="nuLinkApprove">Apply</button>
      </div>
      <div class="response" v-if="responseShow">
        <p class="res-title">Response:</p>
        <div>
          <JsonViewer :value="approveData" sort theme="dark" class="json-viewer-container"/>
        </div>
      </div>
    </div>
    <div class="box">
      <div class="code-style">Code:</div>
      <div>
        <pre v-highlightjs><code class="javascript">{{ approveCode }}</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import {ref} from "vue";
import {JsonViewer} from "vue3-json-viewer"
import { approve } from "@nulink_network/nulink-web-agent-access-sdk"
import {message} from "ant-design-vue";

const responseShow = ref(false)
const applyId = ref('')
const applyUserId = ref('')
const applyUserAddress = ref('')
const days = ref()

const approveData = ref()
const approveCode = 'import { approve } from "@nulink_network/nulink-web-agent-access-sdk"\n' +
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

const nuLinkApprove= async () => {
  await approve(applyId.value,applyUserAddress.value, applyUserId.value, days.value, async (responseData) => {
    if (responseData) {
      // Do something with the responseData
      console.log(responseData);
    } else {
      // Handle the error case
      message.error("Failed to approve")
      console.error('Failed to approve');
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