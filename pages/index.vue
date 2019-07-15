<template>
  <section>
    <b-button
      type="is-success"
      size="is-small"
      icon-left="plus"
      @click="isResidentCreateFormModalActive = true"
    >
      住人を追加
    </b-button>

    <resident-table
      :residents="residents"
      @deleteResident="deleteResident($event)"
    />

    <b-modal :active.sync="isResidentCreateFormModalActive" has-modal-card>
      <resident-create-form-modal @createResident="createResident($event)" />
    </b-modal>
  </section>
</template>

<script>
import residentTable from '~/components/ResidentTable'
import ResidentCreateFormModal from '~/components/ResidentCreateFormModal'

export default {
  components: {
    residentTable,
    ResidentCreateFormModal
  },
  data() {
    return {
      residents: [],
      isResidentCreateFormModalActive: false
    }
  },
  async created() {
    await this.initResidents()
  },
  methods: {
    async initResidents() {
      const { data } = await this.$axios.$get('residents')
      this.residents = data
    },
    async deleteResident(residentId) {
      await this.$dialog.confirm({
        title: '住人を削除しますか？',
        message: 'この操作は取り消すことが出来ません。よろしいですか？',
        confirmText: '削除する',
        cancelText: 'キャンセル',
        type: 'is-danger',
        hasIcon: true,
        onConfirm: async () => {
          await this.$axios.$delete(`residents/${residentId}`)
          this.initResident()
        }
      })
    },
    async createResident(form) {
      await this.$axios.$post('residents', {
        name: form.name
      })
      this.isResidentCreateFormModalActive = false
      this.initResidents()
    }
  }
}
</script>
