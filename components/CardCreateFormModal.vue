<template>
  <form @submit.prevent>
    <div class="modal-card" style="width: auto">
      <header class="modal-card-head">
        <p class="modal-card-title">
          ICカードを追加
        </p>
      </header>
      <section class="modal-card-body">
        {{ diffMin }}分前に未登録のカードがタッチされました。<br />
        このカードを{{ resident.name }}さんに登録します
        <b-field label="ICカード名">
          <b-input
            v-model="formData.name"
            placeholder="ICカード名を入力"
            required
          />
        </b-field>
      </section>
      <footer class="modal-card-foot">
        <button class="button" type="button" @click="$parent.close()">
          キャンセル
        </button>
        <button
          class="button is-primary"
          @click="$emit('createCard', formData)"
        >
          追加する
        </button>
      </footer>
    </div>
  </form>
</template>

<script>
import moment from 'moment'

export default {
  props: {
    resident: {
      type: Object,
      default: null
    }
  },
  data() {
    return {
      formData: {
        name: ''
      },
      lastUnknowTouchIdmDate: ''
    }
  },
  computed: {
    diffMin() {
      const now = moment()
      return now.diff(moment(this.lastUnknowTouchIdmDate), 'minutes')
    }
  },
  async created() {
    const { data } = await this.$axios.$get('last-unknown-touch-idm')
    this.lastUnknowTouchIdmDate = data.created_at
  }
}
</script>

<style></style>
