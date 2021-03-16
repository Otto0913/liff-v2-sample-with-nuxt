<template>
  <v-container>
    <v-card class="mx-auto" max-width="344" outlined>
      <v-list-item three-line>
        <v-list-item-content>
          <div class="overline mb-4">
            OVERLINE
          </div>
          <v-list-item-title class="headline mb-1">
            Content {{ id }}
          </v-list-item-title>
          <v-list-item-subtitle
            >Greyhound divisely hello coldly fonwderfully</v-list-item-subtitle
          >
        </v-list-item-content>

        <v-list-item-avatar tile size="80" color="grey"></v-list-item-avatar>
      </v-list-item>

      <v-card-actions>
        <v-btn outlined rounded text>
          Button
        </v-btn>
      </v-card-actions>
    </v-card>
    <v-card class="mt-5">
      <section class="container">
        <p class="line-id">LINE ID：{{ lineId }}</p>
        <p class="line-name">name：{{ displayName }}</p>
      </section>
    </v-card>
  </v-container>
</template>

<script>
import liff from "@line/liff"

export default {
  data() {
    return {
      id: null,
      lineId: null,
      displayName: null
    }
  },

  computed: {},
  mounted() {
    this.id = this.$route.params["id"]
    console.log(this.id)
    if (liff.isLoggedIn()) {
      liff
        .getProfile()
        .then(profile => {
          this.lineId = profile.userId
          this.displayName = profile.displayName
        })
        .catch(err => {
          alert(err)
          console.log("error", err)
        })
    }
  }
}
</script>
