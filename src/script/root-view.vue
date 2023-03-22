<script setup lang="ts">
import { useElementVisibility } from '@vueuse/core';
import { ref } from 'vue';
const elmTop = ref<HTMLElement | null>(null);
const elmBottom = ref<HTMLElement | null>(null);
const elmBottomIsVisible = useElementVisibility(elmBottom);
const bottomScroll = () => {
  if (elmBottom.value === null) return;
  elmBottom.value.scrollIntoView({
    behavior: 'smooth',
    block: 'center',
    inline: 'center',
  });
};
const topScroll = () => {
  if (elmTop.value === null) return;
  elmTop.value.scrollIntoView({
    behavior: 'smooth',
    block: 'start',
    inline: 'center',
  });
};
</script>
<template>
  <div class="container-fluid">
    <div class="card mt-2 mb-3" ref="elmTop">
      <div class="card-header bg-info">見えないところにある要素を超アピールしてくるアレ</div>
      <div class="card-body">
        Bing Chatで教えてもらったPoem（深い意味はないw） とりあえずスクロールする領域の高さを作りたかっただけ。
        <div class="title">その①</div>
        <div class="poems">
          The Lake Isle of Innisfree I will arise and go now, and go to Innisfree, And a small cabin build there, of
          clay and wattles made: Nine bean-rows will I have there, a hive for the honey-bee; And live alone in the
          bee-loud glade. And I shall have some peace there, for peace comes dropping slow, Dropping from the veils of
          the morning to where the cricket sings; There midnight's all a glimmer, and noon a purple glow, And evening
          full of the linnet's wings. I will arise and go now, for always night and day I hear lake water lapping with
          low sounds by the shore; While I stand on the roadway, or on the pavements grey, I hear it in the deep heart's
          core.
        </div>
        <div class="title">その②</div>
        <div class="poems">
          Shall I compare thee to a summer’s day? Thou art more lovely and more temperate: Rough winds do shake the
          darling buds of May, And summer’s lease hath all too short a date:
        </div>
        <div class="title">その③</div>
        <div class="poems">
          Let me not to the marriage of true minds Admit impediments. Love is not love Which alters when it alteration
          finds, Or bends with the remover to remove:
        </div>
      </div>
      <div class="card-body">
        <button type="button" class="btn btn-favo" ref="elmBottom" @click="topScroll">Favo</button>
      </div>
    </div>
  </div>
  <teleport to="#teleport">
    <div class="pop-up" @click="bottomScroll()" :class="{ isShow: !elmBottomIsVisible }">
      <i class="fas fa-angle-double-down" style="--data-delay: 0ms"></i>
      <i class="fas fa-angle-double-down" style="--data-delay: 100ms"></i>
      <i class="fas fa-angle-double-down" style="--data-delay: 200ms"></i>
      <span>Favo!</span>
      <i class="fas fa-angle-double-down" style="--data-delay: 200ms"></i>
      <i class="fas fa-angle-double-down" style="--data-delay: 100ms"></i>
      <i class="fas fa-angle-double-down" style="--data-delay: 0ms"></i>
    </div>
  </teleport>
</template>

<style lang="scss">
@keyframes pikopiko {
  0% {
    transform: translate(0, 0);
  }
  50% {
    transform: translate(0, -5px);
  }
  100% {
    transform: translate(0, 0);
  }
}
</style>
<style lang="scss" scoped>
.pop-up {
  position: fixed;
  inset: auto auto 0 0;
  width: auto;
  height: 40px;
  padding: 10px;
  background-color: rgb(253, 87, 114);
  border-radius: 0 10px 0 0;
  color: white;
  transform: translateY(40px);
  transition: all 400ms;
  cursor: pointer;
  &.isShow {
    transform: translateY(0);
    > i {
      animation: pikopiko 300ms infinite linear alternate;
      animation-delay: var(--data-delay);
    }
  }
}
.btn-favo {
  background-color: rgb(243, 169, 182);
  color: rgb(255, 255, 255);
  &:hover {
    background-color: rgb(255, 212, 220);
  }
  &:active {
    background-color: rgb(248, 158, 174);
  }
}
.title {
  margin: 10px 0 0 0;
  font-size: 12px;
  background-color: gray;
  color: white;
}

.card {
  max-width: 300px;
}
.card,
.card-header,
.card-body {
  border-color: rgb(24, 7, 112);
}
</style>
