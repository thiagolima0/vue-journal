<template>
  <main class="container m-auto p-10">
    <TheHeader />
    <EntryEditor @@create="handleCreateEntry" />
    <ul>
      <li v-for="entry in entryList" :key="entry.id">
        <EntryCard :entry="entry" />
      </li>
    </ul>
  </main>
</template>

<script setup lang="ts">
import TheHeader from "@/components/TheHeader.vue";
import EntryEditor from "./components/EntryEditor.vue";
import EntryCard from "@/components/EntryCard.vue";
import { reactive } from "vue";
import type User from "./types/User";
import type Entry from "./types/Entry";

const user: User = reactive({
  id: 1,
  username: "daniel",
  settings: [],
});

const entryList: Entry[] = reactive([]);

const handleCreateEntry = (entry: Entry) => {
  entryList.unshift(entry)
};
</script>
