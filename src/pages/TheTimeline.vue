<script setup>
import TimelineItem from '../components/TimelineItem.vue'
import { validateTimelineItems, validateSelectOptions } from '@/validators'

defineProps({
  timelineItems: {
    required: true,
    type: Array,
    validator: validateTimelineItems
  },
  activitySelectOptions: {
    required: true,
    type: Array,
    validator: validateSelectOptions
  }
})
</script>

<template>
  <div class="mt-7">
    <ul>
      <TimelineItem
        v-for="timelineItem in timelineItems"
        :key="timelineItem.hour"
        :activity-select-options="activitySelectOptions"
        :timeline-item="timelineItem" />
    </ul>
  </div>
</template>
