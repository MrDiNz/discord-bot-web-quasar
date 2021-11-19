<template>
  <q-page>
    <div class="row justify-center">
      <q-input outlined type="textarea" v-model="text" class="col-12" />
      <q-btn class="col-auto" color="primary" @click="postToDiscord">
        post
      </q-btn>
    </div>
  </q-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'PageIndex',
  components: {},
  data() {
    return {
      text: ''
    }
  },
  methods: {
    async postToDiscord() {
      await this.$axios.post(process.env.webhook_url as string, {
        content: this.text
      })
    }
  }
})
</script>
