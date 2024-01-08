<script lang="ts">
import {
    ref,
    defineComponent
} from "vue";

const date = ref("");

function getDate() {
    date.value = new Date().toLocaleString("en-GB", {
        weekday: "long",
        day: "numeric",
        month: "short",
        year: "numeric",
    });
}

getDate();

export default defineComponent({
    name: 'Locale',
    setup() {
        return {
            date,
        };
    },
})
</script>

<template>
<!-- insert date like Wednesday, 19 December 2023 -->
<div class="absolute top-10 right-3
bg-[#D9D9D9] rounded-full
bg-opacity-20
px-10 py-2
text-white text-xl
font-['Poppins',_sans-serif]">
    <p>{{ date }}</p>
</div>
</template>
