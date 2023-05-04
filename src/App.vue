<script setup lang="ts">
import TheHeader from "@/components/TheHeader.vue";
import EntryEditor from "./components/EntryEditor.vue";
import EntryCard from "@/components/EntryCard.vue";
import { inject, provide, reactive } from 'vue'
import type User from './types/User'
import type Entry from "./types/Entry";
import { userInjectionKey } from './injectionKeys'

const entries: Entry[] = reactive([])
// const userInjectionKey = Symbol() as InjectionKey<User>
const user : User = reactive({
  id: 1,
  username: 'Asgar',
  settings: []
})

provide(userInjectionKey, user)

// in child component
// const injectedUser = inject(userInjectionKey)


const handleCreateEntry = (entry: Entry) => {
  entries.unshift(entry)
}

</script>

<template>
  <main class="container m-auto p-10">
    Vue js Forge
    <TheHeader />
    <EntryEditor @@create="handleCreateEntry" />
    <ul>
      <li v-for="entry in entries" :key="entry.id">
        <EntryCard :entry="entry" />
      </li>
    </ul>
  </main>
</template>
