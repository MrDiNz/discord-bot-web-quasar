<template>
  <q-page>
    <div class="row justify-center">
      <div class="col-4 q-pt-sm text-h5">
        Post anything too Seekster's discord anonymously (no one know who post
        that)
      </div>
      <div class="col-12 q-pa-sm"></div>
      <q-input v-model="text" class="col-4" outlined type="textarea" />
      <div class="col-12 q-pa-sm"></div>
      <q-select
        :model-value="''"
        :options="userFilterList"
        class="col-4"
        emit-value
        label="tag someone"
        option-label="name"
        option-value="id"
        outlined
        use-input
        @filter="filterFn"
        @update:model-value="onSelected"
      />
      <div class="col-12 q-pa-sm"></div>
      <q-btn class="col-4" color="primary" @click="postToDiscord">
        post to discord
        <q-icon class="q-pl-sm" name="fab fa-discord" />
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
      text: '',
      userList: [
        {
          name: 'Earn - Seekster(PM)',
          id: '812003412501463040'
        },
        {
          name: 'Long - Seektown(PO)',
          id: '627188740149739520'
        },
        {
          name: 'Aof - Seekster(Dev)',
          id: '816715974014533752'
        },
        {
          name: 'Book - Seekster(Dev)',
          id: '870629569902825543'
        },
        {
          name: 'Chai - Seektown(BD)',
          id: '816865036496404480'
        },
        {
          name: 'Chris - Seekster(Dev)',
          id: '852516426032218123'
        },
        {
          name: 'ClickUp',
          id: '758393254944702516'
        },
        {
          name: 'Drink - Seektown(Dev)',
          id: '312074059024302090'
        },
        {
          name: 'Fah - Seekster (Designer)',
          id: '865579569603280898'
        },
        {
          name: 'Faith - CTO',
          id: '442034117144477697'
        },
        {
          name: 'Nice - Data',
          id: '817307862144909333'
        },
        {
          name: 'Pakgad - Seektown(Design)',
          id: '793509628075573299'
        },
        {
          name: 'Phirun - Seektown(Dev)',
          id: '704293243923464253'
        },
        {
          name: 'Ball - Seekster(Dev)',
          id: '142263132226584576'
        },
        {
          name: 'Din - Seektown(Dev)',
          id: '282576853427027968'
        },
        {
          name: 'Goi - WF',
          id: '839784956330901505'
        },
        {
          name: 'Ham - Seektown(Dev)',
          id: '835108122531069952'
        },
        {
          name: 'Jinny - WF',
          id: '256760356083335169'
        },
        {
          name: 'JoeZ',
          id: '715867593147285555'
        },
        {
          name: 'Mean - DevOp',
          id: '509045352893251584'
        },
        {
          name: 'Yuriy - CEO',
          id: '858249056756695061'
        },
        {
          name: 'ZUMBIE',
          id: '750673203315212379'
        }
      ],
      userFilterList: [] as { name: string; id: string }[]
    }
  },
  methods: {
    onSelected(v: string) {
      this.text += ` <@${v}> `
      this.userFilterList = this.userList
    },
    filterFn(val: string, update: (arg0: () => void) => void) {
      console.log(val)
      update(() => {
        this.userFilterList = this.userList.filter(
          (user: { name: string; id: string }) =>
            user.name.toLowerCase().includes(val.toLowerCase())
        )
      })
    },
    async postToDiscord() {
      this.$q.loading.show()
      await this.$axios
        .post(process.env.webhook_url as string, {
          content: this.text
        })
        .then((res) => {
          console.log(res.data)
          this.text = ''
        })
        .finally(() => {
          this.$q.loading.hide()
        })
    }
  }
})
</script>
