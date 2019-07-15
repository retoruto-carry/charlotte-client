<template>
  <section>
    <resident-table
      :residents="residents"
      @deleteResident="deleteResident($event)"
    />
  </section>
</template>

<script>
import residentTable from '~/components/ResidentTable'
export default {
  components: {
    residentTable
  },
  data() {
    return {
      residents: []
    }
  },
  async created() {
    const { data } = await this.$axios.$get('http://localhost/api/residents/')
    this.residents = data
  },
  methods: {
    deleteResident(event) {
      alert(event)
    }
  }
}
</script>
