<script setup lang="ts">
const periods = ["Today", "This week", "This Month"];
</script>

<template>
  <nav class="is-primary panel">
    <span class="panel-tabs">
      <a v-for="period of periods" v-bind:key="period">
        {{ period }}
      </a>
    </span>
  </nav>
</template>
