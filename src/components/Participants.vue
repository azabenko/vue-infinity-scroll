<template>
  <table class="table">
    <thead class="table__header">
      <tr>
        <th></th>
        <th>Participant</th>
        <th>Work Email</th>
        <th>Signed Up</th>
      </tr>
    </thead>
    <tbody class="table__body">
      <tr v-for="participant in participants" :key="participant.id" class="participant">
        <td><img class="participant__avatar" width="48" height="48" :alt="participant.name" :src="participant.avatar"/></td>
        <td>{{ participant.name }}</td>
        <td>{{ participant.email }}</td>
        <td>{{ participant.signedUp }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "Participants",
  props: {
    participants: Array
  }
}
</script>

<style scoped>
  .table {
    width: 100%;
    border-collapse: collapse;
    text-align: left;
  }

  .table__header {
    font-size: 12px;
    line-height: 24px;
    color: #808080;
  }

  .table th {
    font-weight: normal;
  }

  .table__body {
    font-size: 20px;
    line-height: 24px;
  }

  .participant__avatar {
    border-radius: 50%;
    padding-left: 20px;
    padding-right: 20px;
  }

  .participant td {
    padding-top: 24px;
    padding-bottom: 24px;
  }
</style>
