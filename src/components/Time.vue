<script lang="ts">
import {
    ref,
    defineComponent
} from "vue";

const hour = ref("");
const minute = ref("");

// make it look like 12:34
function getTime() {
    hour.value = new Date().getHours().toString().padStart(2, "0");
    minute.value = new Date().getMinutes().toString().padStart(2, "0");
}

getTime();
setInterval(getTime, 1000);

export default defineComponent({
    name: 'Time',
    setup() {
        return {
            hour,
            minute,
        };
    },
})
</script>

<template>
<div class="
        absolute top-10 left-10
        flex justify-center items-center
        px-7 py-7
        rounded-3xl
        bg-[#D9D9D9] bg-opacity-20
        font-['Poppins', sans-serif] text-white text-6xl
        ">
    {{ hour }} <span class="animate-pulse">:</span> {{ minute }}
</div>
</template>
