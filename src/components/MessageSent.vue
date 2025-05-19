<template>
  <section class="sent">
    <header>
      <img src="@/assets/images/icon-success-check.svg" alt="">
      <h2>Message Sent!</h2>
    </header>
    <p>Thanks for completing the form. We'll be in touch soon!</p>
  </section>
</template>

<script>
export default {
  name: 'MessageSent'
}
</script>

<style lang="less" scoped>
.sent {
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  background-color: hsl(187, 24%, 22%);
  color: #fff;
  border-radius: 0 0 10px 10px;
  header {
    display: flex;
    align-items: center;
    h2 {
      margin-left: 10px;
      font-size: 18px;
    }
    margin-bottom: 12px;
  }
}
@media (min-width: 738px) {
  .sent {
    width: 415px;
    height: 108px;
    top: 25px;
    left: 50%;
    transform: translateX(-50%);
    border-radius: 10px;
    padding: 22px 25px;
    font-size: 15px;
  }
}
</style>
