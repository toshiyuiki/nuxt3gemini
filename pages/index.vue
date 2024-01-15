<template>
    <div class="wrap">
        <div class="sec__in__s">
            <h1>Gemini Chat</h1>
            <ul id="chat">
                <li v-for="msgval in msg">
                    <div v-html="msgval" />
                </li>
            </ul>
            <div class="prompt dp__flex">
                <input v-model="prompt" placeholder="メッセージを入力してください">
                <button @click="res">発言</button>
            </div>
        </div>
    </div>
</template>
<script lang="ts" setup>
import {marked} from 'marked';
let msg = ref<any[any]>([]);
const prompt = ref<any>();
const apikey = useRuntimeConfig().public.apikey;
async function res() {
    msg.value.push(`<div class="user">${prompt.value}</div>`);
    const response = await fetch(
        `https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent?key=${apikey}`,{
            method: 'POST',
            body: JSON.stringify({
                contents: [{ parts: [{ text: prompt.value }] }]
            }),
            headers: {
                "Content-Type": "application/json",
            },
        },
    );
    const data = await response.json();
    msg.value.push(`<div class="ai">${marked(data.candidates[0].content.parts[0].text)}</div>`);
    prompt.value = '';
}
</script>
<style lang="scss">
    h1{
        padding:20px 0;
    }
    #chat{
        padding:20px;
        height:500px;
        overflow-y: scroll;
        border:1px solid #ccc;
        margin:0 0 20px;
    }
    #chat li{
        margin:0 0 10px;
        border-radius: 10px;
        overflow: hidden;
    }
    #chat li .user{
        background:#000;
        padding:10px;
        color:#fff;
    }
    #chat li .ai{
        border:1px solid #ffffe0;
    }
    .prompt{
        gap:0 20px;
    }
    .prompt button{
        width:20%;
        text-align:center;
        padding:20px;
        box-sizing: border-box;
        font-size:1.8rem;
    }
    .prompt input{
        width:80%;
        display:block;
        padding:20px;
        box-sizing: border-box;
        font-size:1.8rem;
    }
    @include sp{
        .wrap{
            padding:0 per(10,375);
        }
        .prompt.dp__flex{
            display:block;
        }
        .prompt button{
            width:100%;
            padding:10px;
        }
        .prompt input{
            width:100%;
            padding:10px;
            margin:0 0 10px;
        }
    }
</style>
