<script setup>
import { ref, onMounted } from 'vue'
import { Notyf } from 'notyf'

const notyf = new Notyf()

const name = ref('')
const email = ref('')
const message = ref('')
const isLoading = ref(false)

const WEB3FORMS_ACCESS_KEY = '89dd4b8a-a3c3-48bd-bc41-df465deaf77a'
const subject = 'New message from Portfolio Contact Form'

onMounted(() => {
  const script = document.createElement('script')
  script.src = 'https://www.google.com/recaptcha/api.js'
  script.async = true
  script.defer = true
  document.head.appendChild(script)
})

const submitForm = async () => {
  const recaptchaToken = grecaptcha.getResponse()

  if (!recaptchaToken) {
    notyf.error('Please verify that you are not a robot')
    return
  }

  isLoading.value = true

  try {
    const response = await fetch('https://api.web3forms.com/submit', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        Accept: 'application/json'
      },
      body: JSON.stringify({
        access_key: WEB3FORMS_ACCESS_KEY,
        subject,
        name: name.value,
        email: email.value,
        message: message.value,
        'g-recaptcha-response': recaptchaToken
      })
    })

    const result = await response.json()

    if (result.success) {
      notyf.success('Message Sent!')
      name.value = ''
      email.value = ''
      message.value = ''
      grecaptcha.reset()
    } else {
      notyf.error('Something went wrong. Please try again.')
    }
  } catch (error) {
    console.log(error)
    notyf.error('Unable to send message. Please try again.')
  } finally {
    isLoading.value = false
  }
}
</script>

<template>
  <section id="contact" class="contact-section">
    <h2 class="section-title">Contact</h2>

    <div class="contact-container">
      <div class="contact-map">
        <iframe
          src="https://www.google.com/maps/embed?pb=!1m14!1m8!1m3!1d966.673726544061!2d120.9871983!3d14.2710066!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x33bd7dca01ab2145%3A0xefed764be5658fee!2sGreenwoods%20WindCrest%20-%20Greenwoods%20Executive%20Village%20Gate%202!5e0!3m2!1sen!2sph!4v1780182614583!5m2!1sen!2sph"
          allowfullscreen=""
          loading="lazy"
          referrerpolicy="no-referrer-when-downgrade">
        </iframe>
      </div>

      <form class="contact-form" @submit.prevent="submitForm">
        <input v-model="name" type="text" name="fullname" placeholder="Full Name" required>
        <input v-model="email" type="email" name="email" placeholder="Email Address" required>
        <textarea v-model="message" name="message" rows="5" placeholder="Your Message" required></textarea>

        <div class="g-recaptcha" data-sitekey="6LeGwwgtAAAAAMj-oaSobNBMlBYhNI-QQfH1pIAo"></div>

        <div class="contact-bottom">
          <div class="social-icons">
            <a href="https://www.linkedin.com/in/chinee-marasigan-092459276/" target="_blank" rel="noopener noreferrer">
              <img src="/images/linkedin.png" alt="LinkedIn">
            </a>
            <a href="https://gitlab.com/" target="_blank" rel="noopener noreferrer">
              <img src="/images/gitlab.png" alt="GitLab">
            </a>
            <a href="https://github.com/chin0408" target="_blank" rel="noopener noreferrer">
              <img src="/images/github.png" alt="GitHub">
            </a>
          </div>

          <button type="submit" class="btn-submit" :disabled="isLoading">
            {{ isLoading ? 'Sending...' : 'Submit' }}
          </button>
        </div>
      </form>
    </div>
  </section>
</template>