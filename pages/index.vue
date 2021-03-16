<template>
  <div>
    <v-row justify="center" align="center">
      <v-col cols="12" sm="8" md="6">
        <div class="text-center">
          <v-list>
            <v-list-item-group>
              <v-list-item
                v-for="(item, i) in items"
                :key="i"
                :to="item.link_to"
              >
                <v-list-item-icon>
                  <v-icon v-text="item.icon"></v-icon>
                </v-list-item-icon>
                <v-list-item-content>
                  <v-list-item-title v-text="item.text"></v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </div>
      </v-col>
    </v-row>
    <div class="mt-5">
      <LiffApp />
    </div>
  </div>
</template>

<script>
import LiffApp from "~/components/LiffApp.vue"

export default {
  components: {
    LiffApp
  },
  data() {
    return {
      items: [
        { text: "00001", icon: "mdi-clock", link_to: "/contents/1" },
        { text: "00002", icon: "mdi-account", link_to: "/contents/2" },
        { text: "00003", icon: "mdi-flag", link_to: "/contents/3" }
      ]
    }
  }
}
</script>
