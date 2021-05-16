<template>
  <div class="progress">
    <div class="progress-bar bg-info" role="progressbar" :style="{width:progress +'%'}" aria-valuenow="50" aria-valuemin="0"
         aria-valuemax="100">
      {{ currentItem }}/10
    </div>
  </div>
</template>
<script>
import {eventBus} from "../main";

export default {
  data() {
    return {
      currentItem: 0,
      progress: 1
    }
  },
  created() {
    eventBus.$on("progressBarUpdate", (currentCount) => {
      this.currentItem = currentCount;
      this.progress = this.currentItem * 10;

    })
  }
}
</script>
