<template>
  <CommonHeader
    ref="headerRef"
    :isIndex="true"
    :showSearch="true"
  ></CommonHeader>
  <div
    id="wrap"
    class="w-full xl:w-[1200px] mx-auto min-h-[calc(100vh-218px)] my-[16px]"
  >
    <slot></slot>
  </div>
  <CommonPendant></CommonPendant>
  <CommonFooter></CommonFooter>
</template>

<script setup lang="ts">
import type { CommonHeader } from '#build/components'

const headerRef = ref<InstanceType<typeof CommonHeader>>(null)

const handleHeaderAnimation = (type: string) => {
  headerRef.value?.headerAnimation(type)
}

const scrollListenerHandler = () => {
  nextTick(() => {
    const wrapTop =
      document.getElementById('wrap')?.getBoundingClientRect().top || 0
    if (wrapTop < 75) {
      handleHeaderAnimation('smaller')
    } else {
      handleHeaderAnimation('larger')
    }
  })
}

onMounted(() => {
  nextTick(() => {
    document.addEventListener('scroll', scrollListenerHandler)
  })
})

onUnmounted(() => {
  document.removeEventListener('scroll', scrollListenerHandler)
})
</script>
<style>
#wrap {
  height: 100%;
  box-sizing: border-box;
  z-index: 10;
  color: #434343;
}
</style>
