<template>
<!-- feed component -->
  <div>
    <FeedPreview url="https://www.gamespot.com/feeds/mashup/"></FeedPreview>
  </div>
</template>
<script>
import FeedPreview from "./../src/FeedPreview";

export default {
  name: "FeedPreviewSandbox",
  components: { FeedPreview }
}  
</script>
<style lang="scss" scoped></style>