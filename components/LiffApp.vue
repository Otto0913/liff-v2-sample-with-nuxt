<template>
  <v-card>
    <section class="container">
      <p>status：{{ progressStatus }}</p>
      <p>browserLanguage：{{ browserLanguage }}</p>
      <p>sdkVersion：{{ sdkVersion }}</p>
      <p>lineVersion：{{ lineVersion }}</p>
      <p>isInClient：{{ isInClient }}</p>
      <p>isLoggedIn：{{ isLoggedIn }}</p>
      <p>deviceOS：{{ deviceOS }}</p>
      <p class="line-id">LINE ID：{{ lineId }}</p>
      <p class="line-name">name：{{ displayName }}</p>
    </section>
  </v-card>
</template>

<script>
import liff from "@line/liff"

export default {
  data() {
    return {
      progressStatus: null,
      browserLanguage: null,
      sdkVersion: null,
      lineVersion: null,
      isInClient: null,
      isLoggedIn: null,
      deviceOS: null,
      lineId: null,
      displayName: null
    }
  },
  created: async function() {
    this.progressStatus = "before init"
    this.isInClient = liff.isInClient()
    await liff.init({
      liffId: process.env.lineLiffId
    })
    this.progressStatus = "success init"
    if (!liff.isInClient()) {
      if (!liff.isLoggedIn()) {
        liff.login()
      }
    }
    this.initializeApp()
    if (this.$route.query.id != null) {
      const link_to = "/contents/" + this.$route.query.id
      this.$router.push(link_to)
    }
  },
  methods: {
    initializeApp: function() {
      this.progressStatus = "start initializeApp"
      this.browserLanguage = liff.getLanguage()
      this.sdkVersion = liff.getVersion()
      this.lineVersion = liff.getLineVersion()
      this.isInClient = liff.isInClient()
      this.isLoggedIn = liff.isLoggedIn()
      this.deviceOS = liff.getOS()
      this.progressStatus = "before getProfile"
      liff
        .getProfile()
        .then(profile => {
          this.progressStatus = "success getProfile"
          this.lineId = profile.userId
          this.displayName = profile.displayName
        })
        .catch(err => {
          this.progressStatus = "failed getProfile"
          console.log("error", err)
        })
    }
  }
}
</script>
