<template>
  <div style="display: flex">
    <div class="box">
      <div class="title-span">
        <span class="title">Description:</span>
        <span>Function to fetch send application files.</span>
      </div>
      <div class="option">
        <div class="option-title">Option:</div>
        <div>
          <div class="input-fileId">
            <a-row>
              <a-col :span="4" style="display: flex;align-items: center">ProposerId:</a-col>
              <a-col :span="10"><a-input v-model:value="proposerId" placeholder="9a9dea3341b787a83686a0d1335de3c07c482f401a82099653977744fb49f075" style="width: 550px"/></a-col>
            </a-row>
          </div>
        </div>
        <button class="upload" @click="nuLinkSendApply">Sent Requests</button>
      </div>
      <div class="response" v-if="responseShow">
        <p class="res-title">Response:</p>
        <div>
          <JsonViewer :value="sendApplyData" sort theme="dark" class="json-viewer-container"/>
        </div>
      </div>
    </div>
    <div class="box">
      <div class="code-style">Code:</div>
      <div>
        <pre v-highlightjs><code class="javascript">{{ sendApplyCode }}</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import {ref} from "vue";
import {JsonViewer} from "vue3-json-viewer"
import { getSendApplyFiles } from "@nulink_network/nulink-web-agent-access-sdk"


const responseShow = ref(false)
const sendApplyData = ref()
const proposerId = ref('')
const sendApplyCode = 'import { getSendApplyFiles }  from "@nulink_network/nulink-web-agent-access-sdk"\n' +
    '\n' +
    '// Parameters\n' +
    '// proposerId: string - Applicant\'s account ID\n' +
    '// status: number - Application status 0:no distinction, \n' +
    '//     1: applying, 2: approved, 3: rejected, 4: in progress, 5: expired\n' +
    '// pageNum: number - the page number\n' +
    '// pageSize: number - the page size\n' +
    '\n' +
    'const _getSendApplyFiles = async () => {\n' +
    '    let result = await getSendApplyFiles(\n' +
    '        proposerId, status, pageNum, pageSize\n' +
    '    );\n' +
    '    console.log(result);\n' +
    '};'

const nuLinkSendApply = async () => {
  let result = await getSendApplyFiles(
      proposerId.value,0,1,12
  );
  responseShow.value = true
  sendApplyData.value = result
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
  width: 100px;
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
.option {
  margin-bottom: 8px;
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