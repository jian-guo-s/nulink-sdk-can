<template>
  <div style="display: flex">
    <div class="box">
      <div class="title-span">
        <span class="title">Description:</span>
        <span>Get the list of files belonging to other users.</span>
      </div>
      <div class="option">
        <span class="option-title">Option:</span>
        <button class="upload" @click="nuLinkGetFiles">GetFiles</button>
      </div>
      <div class="response" v-if="responseShow">
        <p class="res-title">Response:</p>
        <div>
          <JsonViewer :value="fileListData"  sort theme="dark" class="json-viewer-container"/>
        </div>
      </div>
    </div>
    <div class="box">
      <div class="code-style">Code:</div>
      <div>
        <pre v-highlightjs><code class="javascript">{{ fileListCode }}</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import {ref} from "vue";
import {JsonViewer} from "vue3-json-viewer"
import { getFileList } from "@nulink_network/nulink-web-agent-access-sdk";

const responseShow = ref(false)
const fileListData = ref()
const fileListCode = 'import { getFileList }  from "@nulink_network/nulink-web-agent-access-sdk"\n' +
    '\n' +
    '// Parameters:\n' +
    '// accountId : string - ID of the currently logged-in user\n' +
    '// include : boolean - If include=false\n' +
    '// desc : boolean - Whether to sort in descending order by upload time\n' +
    '// pageNum : number - page number (starting from 1)\n' +
    '// pageSize : number - page size\n' +
    '\n' +
    'const pageChange = async () => {\n' +
    '    let result = await getFileList(\n' +
    '        accountId, include, desc, pageNum, pageSize\n' +
    '    );\n' +
    '    console.log(result)\n' +
    '};\n'

const nuLinkGetFiles = async () => {
  const account = localStorage.getItem("nulink_agent_react_userinfo")
  let accountId = ""
  if (account) {
    accountId = JSON.parse(account).accountId
  }
  let result =  await getFileList(accountId, true, true, 1, 12);
  responseShow.value = true
  fileListData.value = result
};

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