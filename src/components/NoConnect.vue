<template>
  <div class="connect">
    <img src="../assets/login_icon.svg" />
    <div>
      <p class="tip">Click Agent button to connect nulink agent</p>
      <p class="tip-two">
        Please refer to
        <a
            class="help-center"
            href="https://docs.nulink.org/products/file_sharing_dapp"
            target="_blank"
        >
          Help Center
        </a>
        for agent instructions
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "NoConnect"
}
</script>

<style scoped lang="less">
.content {
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: space-between;
  padding: 40px 120px;
  isolation: isolate;
  min-width: 480px;
  min-height: 349px;
  background: #FAF9FF;
}
.help-center {
  color: #df9100;
}
.tip-two {
  color: #333;
  font-size: 18px;
  font-weight: 600;
  line-height: 24px;
  margin-top: 32px;
}
.tip {
  align-items: center;
  color: #df9100;
  font-size: 36px;
  font-weight: 700;
  line-height: 39px;
}
</style>