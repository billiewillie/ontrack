<script setup>
import { ref } from 'vue'

import { PAGE_ACTIVITIES, PAGE_TIMELINE, PAGE_PROGRESS } from './constants'

import {
  normalizePageHash,
  generateTimelineItems,
  generateActivitySelectOptions
} from './functions'

import TheHeader from './components/TheHeader.vue'
import TheNav from './components/TheNav.vue'

import TheTimeline from './pages/TheTimeline.vue'
import TheActivities from './pages/TheActivities.vue'
import TheProgress from './pages/TheProgress.vue'

const currentPage = ref(normalizePageHash())

const activities = ref(['Coding', 'Reading', 'Training'])

const activitySelectOptions = generateActivitySelectOptions(activities.value)

function goTo(page) {
  currentPage.value = page
}

function createActivity(activity) {
  activities.value.push(activity)
}

function deleteActivity(activity) {
  activities.value.splice(activities.value.indexOf(activity), 1)
}

const timelineItems = generateTimelineItems()
</script>

<template>
  <TheHeader @navigate="goTo($event)" />

  <main class="flex flex-grow flex-col">
    <TheTimeline
      v-show="currentPage === PAGE_TIMELINE"
      :timeline-items="timelineItems"
      :activity-select-options="activitySelectOptions" />
    <TheActivities
      v-show="currentPage === PAGE_ACTIVITIES"
      :activities="activities"
      @create-activity="createActivity"
      @delete-activity="deleteActivity" />
    <TheProgress v-show="currentPage === PAGE_PROGRESS" />
  </main>

  <TheNav
    :current-page="currentPage"
    @navigate="goTo($event)" />
</template>
