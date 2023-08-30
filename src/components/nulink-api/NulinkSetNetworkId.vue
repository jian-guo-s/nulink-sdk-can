<template>
  <div style="display: flex">
    <div class="box">
      <div class="title-span">
        <span class="title">Description:</span>
        <span>Function to set the network info.</span>
      </div>
      <div class="option">
        <div class="option-title">Option:</div>
        <div class="input-fileId">
          <a-row>
            <a-col :span="4" style="display: flex;align-items: center">ChainId:</a-col>
            <a-col :span="10"><a-input v-model:value="chainId" placeholder="97" style="width: 120px"/></a-col>
          </a-row>
        </div>
        <button class="connect" @click="nuLinkSetNetworkId">Set Network Id</button>
      </div>
    </div>
    <div class="box">
      <div class="code-style">Code:</div>
      <div>
        <pre v-highlightjs><code class="javascript">{{ setNetWorkIdCode }}</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { setNetWorkChainId } from "@nulink_network/nulink-web-agent-access-sdk"
import {ref} from "vue";

const chainId = ref()
const setNetWorkIdCode = 'import { setNetWorkChainId }  from "@nulink_network/nulink-web-agent-access-sdk"\n' +
    '\n' +
    '// Parameters\n' +
    '// chainId : string - the network chain id which you will set\n' +
    '\n' +
    'const _setNetWorkChainId = async () => {\n' +
    '    await setNetWorkChainId(97);\n' +
    '    // do something\n' +
    '};'

const nuLinkSetNetworkId = async () => {
  await setNetWorkChainId(chainId.value);
}
</script>

<style scoped lang="less">
.box {
  flex: 1;
  padding: 0 8px;
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
}
.input-fileId {
  margin-bottom: 8px;
}
.title {
  font-size: 14px;
  font-weight: 800;
  margin-right: 4px;
}
.title-span {
  margin-bottom: 8px;
}
.code-style {
  font-size: 14px;
  font-weight: 800;
  margin-bottom: 8px;
}
</style>