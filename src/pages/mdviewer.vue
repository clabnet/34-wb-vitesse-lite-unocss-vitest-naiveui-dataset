<template>
    <MdDocument />
</template>
  
<script>
import MdDocument from "@/data/docker.md";

export default {
    components: {
        MdDocument,
    },
}
</script>


<route lang="yaml">
  meta:
    menuTitle: Markdown viewer
    menuOrderNo: 500
</route>