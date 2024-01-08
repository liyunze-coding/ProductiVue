<script lang="ts">
import {
    StreamerbotClient
} from "@streamerbot/client";
import {
    ref,
    defineComponent
} from "vue";

interface ChatMessage {
    user: string;
    message: string;
}

export default defineComponent({
    name: 'StreamChat',
    setup() {
        const streamChat = ref([] as ChatMessage[]);

        const onData = (data: any) => {
            if (!data.event) return;
            if (data.event.source === "YouTube" && data.event.type === "Message") {
                const payload = data.data;
                // const source:string = data.event.source.toLowerCase();
                const user: string = payload.user.name;

                pushToChat(user, payload.message);
            } else if (
                data.event.source === "Twitch" &&
                data.event.type === "ChatMessage"
            ) {
                const payload = data.data;
                // const source = data.event.source.toLowerCase();
                const user = payload.message.displayName;

                pushToChat(user, payload.message.message)
            }
        }

        new StreamerbotClient({
            host: '127.0.0.1',
            port: 6968,
            endpoint: '/',
            subscribe: {
                YouTube: ["Message"],
                Twitch: ["ChatMessage", "RewardRedemption"],
            },
            onData: onData,
        });

        const pushToChat = (user: string, message: string) => {
            if (streamChat.value.length >= 6) {
                streamChat.value.shift();
            }
            streamChat.value.push({
                user,
                message
            });
        }

        return {
            streamChat,
        };
    },
});
</script>

<template>
<div class="
        absolute bottom-3 right-3
        flex flex-col justify-end items-start
        w-1/4 h-4/5
        overflow-hidden
    ">
    <div v-for="(chat, index) in streamChat" :key="index" class="w-full">
        <!-- <p class="text-white">{{ chat.user }}: {{ chat.message }}</p> -->
        <div class="
                w-full 
                rounded-xl
                bg-[#e5e5e5] bg-opacity-40 text-white font-['Poppins', sans-serif]
                px-3 py-2 mt-1
                flex flex-row justify-start items-start
                ">
            <div class="text-gray-100 font-semibold">{{ chat.user }}</div>
            <span class="mr-2">:</span>
            <div class="text-gray-100">{{ chat.message }}</div>
        </div>
    </div>
</div>
</template>
