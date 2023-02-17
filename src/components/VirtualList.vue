<template>
    <div>虚拟列表</div>
    <div>{{ message }}</div>
    <div ref="listWrap" class="list-wrap" @scroll="scrollListener()">
        <div ref="List" class="list">
            <div 
                class="list-item" 
                v-for="(item, id) in showList" 
                :key="id">
            {{ item }}
            </div>
        </div>
    </div>
</template>
<script lang="ts">
import { ref, onMounted, computed, defineComponent } from 'vue'
export default defineComponent({
    props: {
        list: [],
        itemHeight: Number,
        showNum: Number,
        start: Number,
        end: Number
    },
    setup(props){
        const message = ref('Hi');
        const list = ref(props.list); //长列表数据
        const itemHeight = ref(props.itemHeight); //item高度
        const showNum = ref(props.showNum); //展示的数据
        const start = ref(props.start); //滚动过程中的开始索引
        const end = ref(props.end); //滚动过程中的结束索引
        const listWrap = ref()
        const List = ref()

        onMounted(() => {
            listWrap.value.style.height = itemHeight.value * showNum.value;
        })
        const showList = computed(()=>{
            return list.value.slice(start.value, end.value)
        })
        const scrollListener = (() => {
            console.log(1)
            let scrollTop = listWrap.value.scrollTop
            start.value = Math.floor(scrollTop/itemHeight.value)
            end.value = start.value + showNum.value
            List.value.style.transform = `translateY(${start.value * itemHeight.value}px)`
        })
        return {
            listWrap,
            scrollListener,
            message,
            showList,
            List
        }
    }
})
// const message = ref('Hi');
// const props = defineProps<{
//     list: Array<number>,
//     itemHeight: number,
//     showNum: number,
//     start: number,
//     end: number
// }>()
// const list = ref(props.list); //长列表数据
// const itemHeight = ref(props.itemHeight); //item高度
// const showNum = ref(props.showNum); //展示的数据
// const start = ref(props.start); //滚动过程中的开始索引
// const end = ref(props.end); //滚动过程中的结束索引
// const listWrap = ref()
// const List = ref()
// onMounted(() => {
//     listWrap.value.style.height = itemHeight.value * showNum.value;
// })
// const showList = computed(()=>{
//     return list.value.slice(start.value, end.value)
// })
// const scrollListener = (() => {
//     let scrollTop = listWrap.value.scrollTop
//     console.log(1)
//     start.value = Math.floor(scrollTop/itemHeight.value)
//     end.value = start.value + showNum.value
//     List.value.style.transform = `translateY(${start.value * itemHeight.value}px)`
// })
</script>
<style lang="scss">
.list {
    border-width: 5px; 
    border-radius: 10px;
    width: 100px;
    height: 300px;
    margin: auto;
    background-color: aliceblue;

    .list-item {
        height: 20px;
        margin-top: 10px;
    }
}
.list-wrap {
    overflow-y: scroll;
    height: 153px;
}
</style>