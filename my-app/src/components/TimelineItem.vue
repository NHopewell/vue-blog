<script setup lang="ts">
import { TimelinePost } from "../posts";
// props are properties
// the contents of defineProps are made automatically available in the template
defineProps<{
  post: TimelinePost;
}>();
</script>

<template>
  <a
    class="panel-block is-flex is-flex-direction-column is-align-items-flex-start"
  >
    <a>{{ post.title }}</a>
    <div>{{ post.created.toFormat("d MMM") }}</div>
  </a>
</template>
