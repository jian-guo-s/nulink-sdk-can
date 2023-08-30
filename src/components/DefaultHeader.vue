<template>
  <div class="default-header">
    <div class="logo">
      <img src="../assets/86815953.jpeg" class="logo-image"/>
      <span>NuLink Tutorial</span>
    </div>
    <div class="account">
      <span>Horus (BSC Testnet)</span>
      <div v-if="login" class="login">
        <span>{{accountAddress }}</span>
        <button @click="logout">Logout</button>
      </div>
      <button v-else @click="goToConnect">Agent</button>
    </div>
  </div>
</template>

<script setup >
  import {ref,defineEmits,onMounted} from "vue";
  import { connect } from "@nulink_network/nulink-web-agent-access-sdk"
  import { message } from 'ant-design-vue'
  const login = ref(false)
  const accountAddress = ref("")
  const emit = defineEmits(["connectEvent"])

  onMounted(()=>{
    getDefault()
  })
  const getDefault = () => {
    const accountInfo = localStorage.getItem("nulink_agent_react_userinfo")
    if (accountInfo) {
      login.value = true
      emit('connectEvent',login.value)
      accountAddress.value = JSON.parse(accountInfo)?.accountAddress
    }
    console.log(accountInfo);
  }
  const goToConnect = async () => {
    await connect(loginSuccessHandler)
  }
  const loginSuccessHandler = async (responseData) => {
    if (responseData) {
      // Do something with the responseData
      accountAddress.value = responseData.accountAddress
      login.value = true
      emit('connectEvent',login.value)
    } else {
      message.error("Failed to login in")
      console.error('Failed to login in');
    }
  }
  const logout = () => {
    login.value = false
    emit('connectEvent',login.value)
    localStorage.clear()
  }
</script>

<style scoped lang="less">
.default-header {
  background: #2b3a4b;
  display: flex;
  justify-content: space-between;
  top: 0;
  padding-left: 32px;
  height: 64px;
  z-index: 1;
  align-items:  center;
}
.account {
  display: flex;
  align-items: center;
  span{
    color: #fff;
    font-weight: 400;
    font-size: 14px;
    margin-right: 16px;
  }
  button{
    color: #fff;
    font-weight: 400;
    font-size: 14px;
    background: #df9100;
    border-radius: 20px;
    height: 40px;
    width: 120px;
    outline: none;
    border: 0px solid transparent;
  }
}
.logo {
  display: flex;
  align-items: center;
  span {
    color: rgb(234, 242, 247);
    font: inherit;
    text-align: inherit;
    font-size: 20px;
    font-weight: 700;
  }
}
.logo-image {
  width: 40px;
  height: 40px;
  margin-right: 8px;
}
</style>