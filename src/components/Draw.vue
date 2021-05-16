<template>
  <div class="draw">
    <div class="draw__left-until-draw">
      <LeftUntilDraw />
    </div>
    <div class="draw__participants">
      <ParticipantsContainer />
    </div>
  </div>
</template>

<script>

import ParticipantsContainer from "./ParticipantsContainer";
import LeftUntilDraw from "./LeftUntilDraw";

export default {
  name: 'Draw',
  components: {
    ParticipantsContainer,
    LeftUntilDraw
  }
}
</script>

<style scoped>
  .draw {
    width: 830px;
    margin: 0 auto;
    padding: 60px 0;
  }

  .draw__left-until-draw {
    margin-bottom: 50px;
  }
</style>
