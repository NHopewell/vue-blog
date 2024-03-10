<script setup lang="ts">
import { ref, computed } from "vue";
import { DateTime } from "luxon";
import { Post, today, thisWeek, thisMonth } from "../posts.ts";
import TimelineItem from "./TimelineItem.vue";

const periods = ["Today", "This Week", "This Month"] as const;
type Period = (typeof periods)[number];

const selectedPeriod = ref<Period>("Today");

const selectPeriod = (period: Period): void => {
  console.log(period);
  selectedPeriod.value = period;
};

const posts = computed(() => {
  return (
    [today, thisWeek, thisMonth]
      // formate datetime of all periods
      .map((post) => {
        return { ...post, created: DateTime.fromISO(post.created) };
      }) // filter list of periods
      .filter((post) => {
        if (selectedPeriod.value === "Today") {
          return post.created >= DateTime.now().minus({ day: 1 });
        } else if (selectedPeriod.value === "This Week") {
          return post.created >= DateTime.now().minus({ week: 1 });
        }
        return post;
      })
  );
});
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

    <TimelineItem 
        v-for="post of posts" 
        :key="post.id" 
        :post="post" 
    />
  </nav>
</template>
