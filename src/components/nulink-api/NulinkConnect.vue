<template>
  <div style="display: flex;">
    <div class="box">
      <div class="title-span">
        <span class="title">Description:</span>
        <span>Connect is used for handling login functionality for nulink web agent. It opens a new window for the user to complete the login process, and then executes the callBackFunc with the login data when the login is successful.</span>
      </div>
      <div class="option">
       <span class="option-title">Option:</span>
        <button class="connect" @click="nuLinkConnect">Connect</button>
      </div>
      <div class="response" v-if="responseShow">
        <p class="res-title">Response:</p>
        <div>
          <JsonViewer :value="connectData" sort theme="dark" class="json-viewer-container"/>
        </div>
      </div>
    </div>
    <div class="box">
      <div class="code-style">Code:</div>
      <div>
        <pre v-highlightjs><code class="javascript">{{ connectCode }}</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { connect } from "@nulink_network/nulink-web-agent-access-sdk"
import {message} from "ant-design-vue";
import {JsonViewer} from "vue3-json-viewer"
import {ref} from "vue";

const responseShow = ref(false)
const connectData = ref()
const connectCode = 'import { connect } from "@nulink_network/nulink-web-agent-access-sdk"\n' +
    '\n' +
    'const gotoConnect = async () => {\n' +
    '    await connect(loginSuccessHandler)\n' +
    '}\n' +
    '\n' +
    'const loginSuccessHandler: CallBackFunc = async (responseData) => {\n' +
    '  if (responseData) {\n' +
    '    // Do something with the responseData\n' +
    '    console.log(responseData);\n' +
    '  } else {\n' +
    '    // Handle the error case\n' +
    '    console.error(\'Failed to login in\');\n' +
    '  }\n' +
    '}'

const nuLinkConnect = async () => {
  await connect(loginSuccessHandler)
}

const loginSuccessHandler = async (responseData) => {
  if (responseData) {
    responseShow.value = true
    connectData.value = responseData
    // Do something with the responseData
  } else {
    message.error("Failed to connect agent")
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
.connect {
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