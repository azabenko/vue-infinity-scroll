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
    const MAX_PARTICIPANTS_COUNT = 50;
    const RESULTS_COUNT = 20;

    const scrollComponent = ref(null)
    const participants = ref([])
    const participantsLoaded = ref(false)

    const transformParticipant = ({name, email, registered, id, picture}) => {
      return {
        id: id.value,
        avatar: picture.thumbnail,
        name: `${name.first} ${name.last}`,
        email,
        signedUp: new Date(registered.date)
      }
    }

    const sortParticipants = (a, b) => {
      return new Date(b.signedUp) - new Date(a.signedUp);
    }

    const fetchParticipants = (results = RESULTS_COUNT) => {
      fetch(`https://randomuser.me/api/?inc=name,email,picture,registered,id&results=${results}&noinfo`)
          .then(response => response.json())
          .then(({ results }) => results.map(participant => transformParticipant(participant)))
          .then((data) => participants.value.push(...data))
          .then(() => participants.value.sort(sortParticipants))
    }

    const handleScroll = () => {
      const element = scrollComponent.value

      if ( element.getBoundingClientRect().bottom < window.innerHeight && participants.value.length < MAX_PARTICIPANTS_COUNT ) {
        const resultsLeft = MAX_PARTICIPANTS_COUNT - participants.value.length;
        const results = resultsLeft > RESULTS_COUNT ? RESULTS_COUNT : resultsLeft;

        fetchParticipants(results);
      }

      if ( participants.value.length >= MAX_PARTICIPANTS_COUNT ) {
        participantsLoaded.value = true;
      }
    }

    const throttledScrollHandler = throttle(handleScroll, 200);

    onMounted(() => {
      window.addEventListener("scroll", throttledScrollHandler)
    })

    onUnmounted(() => {
      window.removeEventListener("scroll", throttledScrollHandler)
    })

    fetchParticipants();

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
