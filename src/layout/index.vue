<template>
  <div :class="classObj" class="app-wrapper" :style="{ '--current-color': theme }">
    <div class="main-container full-width">
      <app-main />
    </div>
  </div>
</template>

<script setup>
import { useWindowSize } from '@vueuse/core'
import { AppMain } from './components'
import useAppStore from '@/store/modules/app'
import useSettingsStore from '@/store/modules/settings'

const settingsStore = useSettingsStore()
const theme = computed(() => settingsStore.theme)
const device = computed(() => useAppStore().device)

const classObj = computed(() => ({
  mobile: device.value === 'mobile'
}))

const { width } = useWindowSize()
const WIDTH = 992 // refer to Bootstrap's responsive design

watchEffect(() => {
  if (width.value - 1 < WIDTH) {
    useAppStore().toggleDevice('mobile')
  } else {
    useAppStore().toggleDevice('desktop')
  }
})
</script>

<style lang="scss" scoped>
  @import "@/assets/styles/mixin.scss";
  @import "@/assets/styles/variables.module.scss";

.app-wrapper {
  @include clearfix;
  position: relative;
  height: 100%;
  width: 100%;

  &.mobile.openSidebar {
    position: fixed;
    top: 0;
  }
}

.drawer-bg {
  background: #000;
  opacity: 0.3;
  width: 100%;
  top: 0;
  height: 100%;
  position: absolute;
  z-index: 999;
}

.main-container.full-width {
  margin-left: 0;
  width: 100%;
}

.hideSidebar .fixed-header {
  width: calc(100% - 54px);
}

.sidebarHide .fixed-header {
  width: 100%;
}

.mobile .fixed-header {
  width: 100%;
}
</style>