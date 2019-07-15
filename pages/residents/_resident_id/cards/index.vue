<template>
  <section>
    <b-button
      type="is-success"
      size="is-small"
      icon-left="plus"
      @click="isCardCreateFormModalActive = true"
    >
      ICカードを追加
    </b-button>

    <card-table :cards="resident.cards" @deleteCard="deleteCard($event)" />

    <b-modal :active.sync="isCardCreateFormModalActive" has-modal-card>
      <card-create-form-modal
        :resident="resident"
        @createCard="createCard($event)"
      />
    </b-modal>
  </section>
</template>

<script>
import CardTable from '~/components/CardTable'
import CardCreateFormModal from '~/components/CardCreateFormModal'

export default {
  components: {
    CardTable,
    CardCreateFormModal
  },
  data() {
    return {
      resident: {
        name: '',
        cards: []
      },
      isCardCreateFormModalActive: false
    }
  },
  async created() {
    await this.initResident()
  },
  methods: {
    async initResident() {
      const { data } = await this.$axios.$get(
        `residents/${this.$route.params.resident_id}`
      )
      this.resident = data
    },
    async deleteCard(cardId) {
      await this.$dialog.confirm({
        title: 'ICカードを削除しますか？',
        message: 'この操作は取り消すことが出来ません。よろしいですか？',
        confirmText: '削除する',
        cancelText: 'キャンセル',
        type: 'is-danger',
        hasIcon: true,
        onConfirm: async () => {
          await this.$axios.$delete(
            `residents/${this.$route.params.resident_id}/cards/${cardId}`
          )
          this.initResident()
        }
      })
    },
    async createCard(form) {
      await this.$axios.$post(
        `residents/${this.$route.params.resident_id}/cards`,
        {
          name: form.name
        }
      )
      this.isCardCreateFormModalActive = false
      this.initResident()
    }
  }
}
</script>
