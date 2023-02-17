<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>
  <VirtualList 
    :list="newList" 
    :itemHeight="20"
    :showNum="10"
    :start="0"
    :end="10"
  />
</template>
<script lang="ts">
import VirtualList from '@/components/VirtualList.vue';
import { defineComponent } from 'vue';
export default defineComponent({
  components: {
    VirtualList,
  },
  setup() {
    const newList:Array<number> = []
    let cnt = 100000
    while(cnt>0) {
      newList.push(cnt)
      cnt-=1
    }
    return {
      newList
    }
  },
})


</script>
