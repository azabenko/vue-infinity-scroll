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
        <td>{{ transformDate(participant.signedUp) }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "ParticipantsList",
  props: {
    participants: Array
  },
  methods: {
    transformDate(date) {
      const ONE_MINUTE = 60 * 1000;
      const ONE_HOUR = 60 * ONE_MINUTE;

      const currDate = new Date();
      const timeLeft = currDate - new Date(date);
      const month = date.toLocaleDateString('en-US', { month: 'short'});
      const isToday = date.toDateString() === (new Date()).toDateString();

      const yesterday = new Date();
      yesterday.setDate(yesterday.getDate() - 1);
      const isYesterday = date.toDateString() === yesterday.toDateString();


      if ( timeLeft < ONE_MINUTE ) {
        return 'just now';
      }

      if ( timeLeft < ONE_HOUR ) {
        return `${Math.floor(timeLeft / ONE_MINUTE)}m ago`;
      }

      if ( isToday ) {
        return `${Math.floor(timeLeft / ONE_HOUR)}h ago`;
      }

      if ( isYesterday ) {
        return 'yesterday';
      }

      if ( date.getFullYear() === currDate.getFullYear() ) {
        return `${date.getDate()} ${month}`
      }

      return `${date.getDate()} ${month} ${date.getFullYear()}`
    }
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
