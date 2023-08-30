<template>
  <div style="display: flex">
    <div class="box">
      <div class="title-span">
        <span class="title">Description:</span>
        <span>Function to get the network info.</span>
      </div>
      <div class="option">
        <span class="option-title">Option:</span>
        <button class="connect" @click="nuLinkGetNetworkId">Get Network Id</button>
      </div>
      <div class="response" v-if="responseShow">
        <p class="res-title">Response:</p>
        <div>
          <JsonViewer :value="networkIdData" boxed sort theme="dark"/>
        </div>
      </div>
    </div>
    <div class="box">
      <div class="code-style">Code:</div>
      <div>
        <pre v-highlightjs><code class="javascript">{{ netWorkIdCode }}</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { getNetWorkChainId } from "@nulink_network/nulink-web-agent-access-sdk"
import {JsonViewer} from "vue3-json-viewer"
import {ref} from "vue";

const responseShow = ref(false)
const networkIdData = ref()
const netWorkIdCode = 'import { getNetWorkChainId }  from "@nulink_network/nulink-web-agent-access-sdk"\n' +
    '\n' +
    'const _getNetWorkChainId = async () => {\n' +
    '    let chainId = await getNetWorkChainId();\n' +
    '    // do something\n' +
    '};'

const nuLinkGetNetworkId = async () => {
  let chainId = await getNetWorkChainId();
  const result = {
    chainId:chainId
  }
  responseShow.value = true
  networkIdData.value = result
}
</script>

<style scoped lang="less">
.box {
  flex: 1;
  padding: 0 8px;
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
</style>