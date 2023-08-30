<template>
  <div class="tutorial">
    <p class="tutorial-title">NuLink Agent SDK Interactive Tutorial</p>
    <div class="tutorial-content">
      <a-collapse v-model:activeKey="activeKey" ghost>
        <a-collapse-panel key="1" header="NuLink Connect" :style="customStyle">
          <NuLinkConnect/>
        </a-collapse-panel>
        <a-collapse-panel key="2" header="NuLink Upload" :style="customStyle">
          <NuLinkUpload/>
        </a-collapse-panel>
        <a-collapse-panel key="3" header="NuLink Get Files" :style="customStyle">
          <NuLinkGetFiles/>
        </a-collapse-panel>
        <a-collapse-panel key="4" header="NuLink File Detail" :style="customStyle">
          <NuLinkFileDetail/>
        </a-collapse-panel>
        <a-collapse-panel key="5" header="NuLink Apply Files" :style="customStyle">
          <NuLinkApply/>
        </a-collapse-panel>
<!--        <a-collapse-panel key="6" header="NuLink Approve Files" :style="customStyle">-->
<!--          <NuLinkApprove/>-->
<!--        </a-collapse-panel>-->
        <a-collapse-panel key="7" header="NuLink Download" :style="customStyle">
          <NuLinkDownload/>
        </a-collapse-panel>
        <a-collapse-panel key="8" header="NuLink Get SendApplyFiles" :style="customStyle">
          <NuLinkSendApply/>
        </a-collapse-panel>
        <a-collapse-panel key="9" header="NuLink Get InComingApplyFiles" :style="customStyle">
          <NuLinkInComingApply/>
        </a-collapse-panel>
        <a-collapse-panel key="10" header="NuLink Get Network Id" :style="customStyle">
          <NuLinkGetId/>
        </a-collapse-panel>
        <a-collapse-panel key="11" header="NuLink Set Network Id" :style="customStyle">
          <NuLinkSetId/>
        </a-collapse-panel>
      </a-collapse>
    </div>
  </div>
</template>

<script setup >
  import NuLinkConnect from "@/components/nulink-api/NulinkConnect";
  import NuLinkUpload from "@/components/nulink-api/NulinkUpload"
  import NuLinkGetFiles from "@/components/nulink-api/NulinkGetFiles"
  import NuLinkFileDetail from "@/components/nulink-api/NulinkFileDetail"
  import NuLinkApply from "@/components/nulink-api/NulinkApply"
  // import NuLinkApprove from "@/components/nulink-api/NulinkApprove"
  import NuLinkDownload from "@/components/nulink-api/NulinkDownload"
  import NuLinkSendApply from "@/components/nulink-api/NulinkSendApply"
  import NuLinkInComingApply from "@/components/nulink-api/NulinkComingApply"
  import NuLinkGetId from "@/components/nulink-api/NulinkGetNetworkId"
  import NuLinkSetId from "@/components/nulink-api/NulinkSetNetworkId"
  import {ref} from "vue";
  const activeKey = ref(['1']);
  const customStyle =
      'background: #f7f7f7;border-radius: 4px;margin-bottom: 24px;border: 0;overflow: hidden';
  const data = ref("")
  console.log(data)
</script>

<style scoped lang="less">
.tutorial {
  background: #FAF9FF;
  padding: 40px 56px;
}
.tutorial-title {
  align-items: center;
  color: #df9100;
  font-size: 36px;
  font-weight: 700;
  line-height: 39px;
  margin-top: 32px;
}
</style>