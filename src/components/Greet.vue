<script setup lang="ts">
import { ref } from "vue";
// import { invoke } from "@tauri-apps/api/tauri";
import { Command } from '@tauri-apps/api/shell'


const greetMsg = ref("");
const name = ref("");

async function greet() {
  let aa = new Command('run-pytool', ['/c','python','--version']);
  aa.stdout.on('data', data => console.log(data)); //成功事件
  aa.stderr.on('data', data => console.log(data)); //失败事件
  aa.on('close', () => {console.log('打包完成')});
  await aa.spawn();
}
</script>

<template>
  <form class="row" @submit.prevent="greet">
    <input id="greet-input" v-model="name" placeholder="Enter a name..." />
    <button type="submit">Greet</button>
  </form>

  <p>{{ greetMsg }}</p>
</template>
