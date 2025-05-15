<template>
  <div class="app">
    <section>
      <h1>Contact Us</h1>
      <form action="#">
        <label for="F-name">First Name</label>
        <input type="text" id="F-name" name="F-name" aria-describedby="fname-error" required>
        <span id="fname-error" class="error-message" :style="{ visibility: isShow ? 'visible' : 'hidden' }">This field is required</span>

        <label for="L-name">Last Name</label>
        <input type="text" id="L-name" name="L-name" aria-describedby="lname-error" required>
        <span id="lname-error" class="error-message" :style="{ visibility: isShow ? 'visible' : 'hidden' }">This field is required</span>

        <label for="email">Email Address</label>
        <input type="email" name="email" id="email" aria-describedby="email-error" required>
        <span id="email-error" class="error-message" v-if="false">Please enter a valid email address</span>
        <span id="email-error" class="error-message" v-else>This field is required</span>

        <fieldset aria-describedby="query-error">
          <legend>Query Type</legend>
          <section>
            <input type="radio" id="enquiry" name="query-type" value="enquiry" required>
            <label for="enquiry">General Enquiry</label>
          </section>
          <section>
            <input type="radio" id="request" name="query-type" value="request" required>
            <label for="request">Support Request</label>
          </section>
          <span id="query-error" class="error-message" :style="{ visibility: isShow ? 'visible' : 'hidden' }">Please select a query type</span>
        </fieldset>

        <label for="message">Message</label>
        <textarea name="message" id="message" cols="30" rows="10" aria-describedby="message-error" required></textarea>
        <span id="message-error" class="error-message" :style="{ visibility: isShow ? 'visible' : 'hidden' }">This field is required</span>

        <div class="checkbox-group">
          <input type="checkbox" name="accept" id="accept" aria-describedby="checkbox-error" required>
          <label for="accept">I consent to being contacted by the team</label>
        </div>
        <span id="checkbox-error" class="error-message" :style="{ visibility: isShow ? 'visible' : 'hidden' }">To submit this form, please consent to being contacted</span>

        <button>Submit</button>
      </form>
    </section>
    <section>
      <h2>Message Sent!</h2>
      <p>Thanks for completing the form. We'll be in touch soon!</p>
    </section>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {
  },
  data () {
    return {
      isShow: false
    }
  }
}
</script>

<style lang="less">
@import '@/assets/styles/styles.less';
</style>
