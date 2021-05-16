<template>
  <div ref="scrollComponent">
    <Participants :participants="participants" />
    <UsersLoaded v-if="participantsLoaded" />
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue'
import Participants from "./Participants";
import UsersLoaded from "./UsersLoaded";
import { throttle } from "lodash";

export default {
  name: 'ParticipantsContainer',
  components: {
    Participants,
    UsersLoaded
  },
  setup () {
    const scrollComponent = ref(null)
    const participants = ref([])
    const participantsLoaded = ref(false)

    const isToday = (date) => {
      return date.toDateString() === (new Date()).toDateString();
    }

    const isYesterday = (date) => {
      const yesterday = new Date();
      yesterday.setDate(date.getDate() - 1);

      return date.toDateString() === yesterday.toDateString();
    }

    const transformDate = (date) => {
      const ONE_MINUTE = 60 * 1000;
      const ONE_HOUR = 60 * ONE_MINUTE;

      const currDate = new Date();
      const timeLeft = currDate - new Date(date);

      if ( timeLeft < ONE_MINUTE ) {
        return 'just now';
      }

      if ( timeLeft < ONE_HOUR ) {
        return date.getMinutes();
      }

      if ( isToday(date) ) {
        return date.getHours();
      }

      if ( isYesterday(date) ) {
        return 'yesterday';
      }

      if ( date.getFullYear() === currDate.getFullYear() ) {
        return date
            .toLocaleDateString('en-US', { day: 'numeric', month: 'short'})
            .split(' ')
            .reverse()
            .join(' ');
      }

      return date.toLocaleDateString('en-US', { year: 'numeric', month: 'short', day: 'numeric' });
    }

    const transformParticipant = ({name, email, registered, id, picture}) => {
      return {
        id: id.value,
        avatar: picture.thumbnail,
        name: `${name.first} ${name.last}`,
        email,
        signedUp: transformDate(new Date(registered.date))
      }
    }

    const fetchParticipants = () => {
      fetch("https://randomuser.me/api/?inc=name,email,picture,registered,id&results=20&noinfo")
          .then(response => response.json())
          .then(({ results }) => results.map(participant => transformParticipant(participant)))
          .then((data) => participants.value.push(...data))
    }

    fetchParticipants();

    const handleScroll = () => {
      const element = scrollComponent.value

      if ( element.getBoundingClientRect().bottom < window.innerHeight && participants.value.length < 50 ) {
        fetchParticipants();
      }

      if ( participants.value.length >= 50 ) {
        participantsLoaded.value = true;
      }
    }

    const foo = throttle(handleScroll, 200);

    onMounted(() => {
      window.addEventListener("scroll", foo)
    })

    onUnmounted(() => {
      window.removeEventListener("scroll", foo)
    })

    return {
      participants,
      scrollComponent,
      participantsLoaded
    }
  },
}
</script>

<style scoped>

</style>
