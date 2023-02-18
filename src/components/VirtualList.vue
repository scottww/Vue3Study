<template>
    <div class="virtual-scroll-list" ref="listRef">
        <div class="list" :style="{ height: `${listHeight}px` }">
            <div :style="`transform: translateY(${translateY}px)`" class="itemContainer">
                <div v-for="(i, index) in realData" :key="index" class="item" :style="{ height: `${itemHeight}px` }">{{ i
                }}</div>
            </div>
        </div>
    </div>
    <div class="info">
        <i>当前开始索引： {{ start }}，结束索引： {{ end }}</i>
    </div>
</template>

<script>
import { ref, onMounted, computed, onBeforeUnmount } from 'vue';
</script>
<script setup>
const data = Array.from({ length: 500 }, (v, k) => `内容${k}`);
const itemHeight = 150;
const listHeight = computed(() => {
    return data.length * itemHeight;
})

// +1准备多一个数据，防止滚动留白
const itemCount = computed(() => {
    return Math.ceil(500 / itemHeight) + 1;
})

const listRef = ref(0);
const srollTop = ref(0);

const start = computed(() => {
    return Math.floor(srollTop.value / itemHeight);
})

const end = computed(() => {
    return start.value + itemCount.value;
})

const realData = computed(() => {
    return data.slice(start.value, end.value);
})

const translateY = computed(() => {
    return start.value * itemHeight;
})
const onScroll = (e) => {
    srollTop.value = e.target.scrollTop;
}
onMounted(() => {
    listRef.value.addEventListener('scroll', onScroll);
})

onBeforeUnmount(() => {
    listRef.value.removeEventListener('scroll', onScroll);

})

</script>

<style scoped>
.virtual-scroll-list {
    position: relative;
    inset: 0;
    margin: 0 auto;

    border: 2px solid orange;
    width: 500px;
    overflow-y: auto;
    max-height: 500px;
}

.item {
    box-sizing: border-box;
    /* background-color: gray; */
    border-bottom: 1px dashed gray;
}
</style>
  