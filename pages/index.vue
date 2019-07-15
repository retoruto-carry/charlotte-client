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
    deleteResident(residentId) {
      alert(residentId)
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
