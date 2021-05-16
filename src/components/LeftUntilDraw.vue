<template>
  <div class="left-until-draw">
    <h2 class="left-until-draw__title">Left until the draw</h2>
    <span class="left-until-draw__time-left">{{ timeLeft }}</span>
  </div>
</template>

<script>
export default {
  name: "LeftUntilDraw",
  setup () {
    const currDay = new Date();
    const endOfDay = new Date();
    endOfDay.setHours(23,59,59,999);

    const timeLeft = `${endOfDay.getHours() - currDay.getHours()}H ${endOfDay.getMinutes() - currDay.getMinutes()}M ${endOfDay.getSeconds() - currDay.getSeconds()}S`;

    return {
      timeLeft
    }
  }
}
</script>

<style scoped>
  .left-until-draw {
    padding: 28px 68px;
    background-color: #F3F3F3;
    border-radius: 24px;
  }

  .left-until-draw__title {
    font-size: 12px;
    line-height: 24px;
  }

  .left-until-draw__time-left {
    font-weight: 600;
    font-size: 56px;
    line-height: 80px;
    text-transform: uppercase;
  }
</style>
