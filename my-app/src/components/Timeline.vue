<script setup lang="ts">
import { ref } from "vue";
import { Post, today, thisWeek, thisMonth } from "../posts.ts";

const periods = ["Today", "This Week", "This Month"] as const;
type Period = (typeof periods)[number];

const selectedPeriod = ref<Period>("Today");

const selectPeriod = (period: Period): void => {
  console.log(period);
  selectedPeriod.value = period;
};

const posts: Post[] = [today, thisWeek, thisMonth];
</script>

<template>
  <nav class="is-primary panel">
    <span class="panel-tabs">
      <a
        v-for="period of periods"
        :key="period"
        :class="{ 'is-active': period === selectedPeriod }"
        @:click="selectPeriod(period)"
      >
        {{ period }}
      </a>
    </span>

    <a v-for="post of posts" :key="post" class="panel-block">
      <a>{{ post.title }}</a>
      <div>{{ post.created }}</div>
    </a>
  </nav>
</template>
