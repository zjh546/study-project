<template>
  <div class="tab-control">
    <template v-for="(item, index) in titles" :key="item">
      <div
        class="tab-control-item"
        :class="{ active: index === currentIndex }"
        @click="itemClick(index)"
      >
        <span>{{ item }}</span>
      </div>
    </template>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits, defineExpose } from "vue";

const props = defineProps({
  titles: {
    type: Array,
    default: () => [],
  },
});

const currentIndex = ref(0);
const emits = defineEmits(["ChangeNameEmit"]);
const itemClick = (index) => {
  currentIndex.value = index;
  emits("ChangeNameEmit", index);
};
const setCurrentIndex = (index) => (currentIndex.value = index);
const getCurrentIndex = () => currentIndex.value;

defineExpose({ setCurrentIndex, getCurrentIndex });
</script>

<style lang="less" scoped>
.tab-control {
  display: flex;
  height: 44px;
  line-height: 44px;
  text-align: center;
  background-color: #fff;
}

.tab-control-item {
  flex: 1;
}

.tab-control-item.active {
  color: var(--primary-color);
  font-weight: 700;
}

.tab-control-item.active span {
  border-bottom: 3px solid var(--primary-color);
  padding: 8px;
}
</style>
