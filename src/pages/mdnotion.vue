<script setup lang="ts">
import { NotionRenderer, getPageBlocks, useGetPageBlocks } from "vue3-notion"
import { ref, onMounted } from "vue"

//const data = ref()
// onMounted(async () => {
//   data.value = await getPageBlocks("4b2dc28a5df74034a943f8c8e639066a")
// })

// ---- or using Composables ----
const { data } = useGetPageBlocks("ab118e1dcb294014b0b84509bf162b68")

// https://www.notion.so/85750ecbe6274ce096bec7b200d4a99b?v=c85fd1868cd84eb7b2f1eb66fe777676

// https://www.notion.so/85750ecbe6274ce096bec7b200d4a99b?v=c85fd1868cd84eb7b2f1eb66fe777676
// https://www.notion.so/Personal-Home-a11a81eb5a0841cf8c8291a50e0c0408
// https://www.notion.so/Quick-Note-93e8e3ff3df549128762e9680368881a
// https://www.notion.so/752f4b4e86e648ffa82b77395c85911f?v=86b4a98ba0614a7ea99a76684a3f5a7b
// https://www.notion.so/0605744b8d69443d97bc67c15fef361f?v=bbe38bb487ec43c088eb2b13862d79fb
// https://www.notion.so/Hello-World-fc6b43935e974fcbb1d7c42f41b9ad74
// https://www.notion.so/PromiseAll-f8080acdcdd649269dec934eddb64b86
// https://www.notion.so/How-Acme-is-saving-the-giant-iguanas-of-Roat-n-0e2df1b9eb8943acaab34900852ce629
// https://www.notion.so/Pomini-Apps-ab118e1dcb294014b0b84509bf162b68
</script>

<template>
  <NotionRenderer v-if="data"
    :blockMap="data"
    fullPage />
</template>

<style>
@import "vue3-notion/dist/style.css";
/* optional Notion-like styles */
@import "prismjs/themes/prism.css";
@import "katex/dist/katex.min.css";
</style>

<route lang="yaml">
  meta:
    menuTitle: Markdown Notion
    menuOrderNo: 550
</route>