<template>
  <div class="app">
    <section>
      <h1>Contact Us</h1>
      <form action="#" @submit.prevent="validateForm">
        <div class="name">
          <div class="fitstN">
            <label for="F-name">First Name</label>
            <input
              type="text"
              id="F-name"
              name="F-name"
              aria-describedby="fname-error"
              v-model="form.firstName"
              @blur="validateField('firstName')"
            >
            <span
              id="fname-error"
              class="error-message"
              v-if="error.firstName"
            >This field is required</span>
            <div aria-hidden v-else class="no-error"></div>
          </div>

          <div class="lastN">
            <label for="L-name">Last Name</label>
            <input
              type="text"
              id="L-name"
              name="L-name"
              aria-describedby="lname-error"
              v-model="form.lastName"
              @blur="validateField('lastName')"
            >
            <span
              id="lname-error"
              class="error-message"
              v-if="error.lastName"
            >This field is required</span>
            <div aria-hidden v-else class="no-error"></div>
          </div>
          </div>

        <label for="email">Email Address</label>
        <input
          type="email"
          name="email"
          id="email"
          aria-describedby="email-error"
          v-model="form.email"
          @blur="validateField('email')"
        >
        <span
          class="error-message"
          v-if="error.email"
        >{{ emailErrorMessage }}</span>
        <div aria-hidden v-else class="no-error"></div>

        <fieldset aria-describedby="query-error">
          <legend>Query Type</legend>
          <section
          @click="form.queryType = 'enquiry'"
    :class="{ 'selected-option': form.queryType === 'enquiry' }">
            <input
              type="radio"
              id="enquiry"
              name="query-type"
              value="enquiry"
              v-model="form.queryType"
              @change="validateField('queryType')"
            >
            <label for="enquiry">General Enquiry</label>
          </section>
          <section
          @click="form.queryType = 'request'"
    :class="{ 'selected-option': form.queryType === 'request' }">
            <input
              type="radio"
              id="request"
              name="query-type"
              value="request"
              v-model="form.queryType"
              @change="validateField('queryType')"
            >
            <label for="request">Support Request</label>
          </section>
          <span
            id="query-error"
            class="error-message"
            v-if="error.queryType"
          >Please select a query type</span>
          <div aria-hidden v-else class="no-error"></div>
        </fieldset>

        <label for="message">Message</label>
        <textarea
          name="message"
          id="message"
          cols="30"
          rows="10"
          aria-describedby="message-error"
          v-model="form.message"
          @blur="validateField('message')"
        >
        </textarea>
        <span
          id="message-error"
          class="error-message"
          v-if="error.message"
        >This field is required</span>
        <div aria-hidden v-else class="no-error"></div>

        <div class="checkbox-group">
          <input
            type="checkbox"
            name="accept"
            id="accept"
            aria-describedby="checkbox-error"
            v-model="form.accept"
            @change="validateField('accept')"
          >
          <label for="accept">I consent to being contacted by the team</label>
        </div>
        <span
          id="checkbox-error"
          class="error-message"
          v-if="error.accept"
        >To submit this form, please consent to being contacted</span>
        <div aria-hidden v-else class="no-error"></div>

        <button aria-busy="true" aria-label="Submit contact form" type="submit">Submit</button>
      </form>
    </section>
    <transition name="fade-only">
      <MessageSent v-if="submitted" />
    </transition>
  </div>
</template>

<script>
import MessageSent from './components/MessageSent.vue'
export default {
  name: 'App',
  components: {
    MessageSent
  },
  data () {
    return {
      form: {
        firstName: '',
        lastName: '',
        email: '',
        queryType: '',
        message: '',
        accept: false
      },
      error: {
        firstName: false,
        lastName: false,
        email: false,
        queryType: false,
        message: false,
        accept: false
      },
      submitted: false
    }
  },
  computed: {
    emailErrorMessage () {
      if (!this.form.email) return 'This field is required'
      const isValid = /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(this.form.email)
      if (!isValid) return 'Please enter a valid email address'
      return ''
    }
  },
  methods: {
    validateField (field) {
      const value = this.form[field]
      switch (field) {
        case 'firstName':
        case 'lastName':
        case 'message':
          this.error[field] = !value.trim()
          break
        case 'email':
          this.error.email = !value || !/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(value)
          break
        case 'queryType':
          this.error.queryType = !value
          break
        case 'accept':
          this.error.accept = !value
          break
      }
    },
    validateForm () {
      const fields = ['firstName', 'lastName', 'email', 'queryType', 'message', 'accept']
      fields.forEach(this.validateField)
      const hasError = Object.values(this.error).some(Boolean)
      if (!hasError) {
        this.submitted = true
        console.log('Form submitted:', this.form)
        // 添加滚动到顶部代码
        window.scrollTo({
          top: 0,
          behavior: 'smooth' // 可选：平滑滚动
        })
        setTimeout(() => {
          this.submitted = false
        }, 1500)
        this.form = {
          firstName: '',
          lastName: '',
          email: '',
          queryType: '',
          message: '',
          accept: false
        }
      }
    }
  }
}
</script>

<style lang="less">
@import '@/assets/styles/styles.less';
</style>
