<template>
    <div>
        <div class="sec__in__s">
            <h1>today's dish</h1>
            <button v-on:click="res">今日のご飯</button>
            <div id="menu" v-html="cook" />
        </div>
    </div>
</template>
<script lang="ts" setup>
import {marked} from 'marked';
const cook = ref();
const apikey = useRuntimeConfig().public.apikey;
async function res() {
    const response = await fetch(
        `https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent?key=${apikey}`,{
            method: 'POST',
            body: JSON.stringify({
                contents: [{ parts: [{ text: "今日の晩御飯は何が良いですか？メニュー一つとレシピを教えてください。" }] }]
            }),
            headers: {
                "Content-Type": "application/json",
            },
        },
    );
    const data = await response.json();
    cook.value = marked(data.candidates[0].content.parts[0].text);
}
</script>
<style lang="scss">
    h1{
        margin:0 0 1em;
    }
    button{
        background:#333;
        color:#fff;
        padding:.5em 1em;
        border-radius: 10px;
        font-size:2.4rem;
        margin:0 0 1em;
        cursor: pointer;
    }
    #menu{
        padding:20px;
        border:1px solid #ccc;
    }
</style>
