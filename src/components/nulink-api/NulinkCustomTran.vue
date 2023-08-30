<template>
  <div style="display: flex">
    <div class="box">
      <div class="title-span">
        <span class="title">Description:</span>
        <span>Send custom transaction by agent website.</span>
      </div>
      <div class="option">
        <div class="option-title">Option:</div>
        <div class="input-fileId">
          <a-row>
            <a-col :span="4" style="display: flex;align-items: center">ToAddress:</a-col>
            <a-col :span="10"> <a-input v-model:value="toAddress" placeholder="0xe2695b1490684d6a786cafc862764b87381ba821" style="width: 400px"/></a-col>
          </a-row>
        </div>
        <button class="upload" @click="nuLinkCustom">Apply</button>
      </div>
      <div class="response" v-if="responseShow">
        <p class="res-title">Response:</p>
        <div>
          <JsonViewer :value="customData" sort theme="dark" class="json-viewer-container"/>
        </div>
      </div>
    </div>
    <div class="box">
      <div class="code-style">Code:</div>
      <div>
        <pre v-highlightjs><code class="javascript">{{ customCode }}</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import {ref} from "vue";
import {JsonViewer} from "vue3-json-viewer"
import { sendCustomTransaction } from "@nulink_network/nulink-web-agent-access-sdk"
import {message} from "ant-design-vue";
const responseShow = ref(false)
const toAddress = ref('')

const customData = ref()
const customCode = 'import { approve } from "@nulink_network/nulink-web-agent-access-sdk"\n' +
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

const nuLinkCustom = async () => {
  await sendCustomTransaction(sendTransactionCallBack, toAddress.value, '', '1000','1')
}
const sendTransactionCallBack = async (data) => {
  try {
    if ('success' == data.result) {
      console.log(data)
    } else {
      message.error("Transaction failed, Please try again")
    }
  } catch (error) {
    message.error("Transaction failed, Please try again")
    console.log(error)
  }
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