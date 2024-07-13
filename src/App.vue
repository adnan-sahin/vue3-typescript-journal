<script setup lang="ts">
import { ref, Ref, provide, inject } from "vue";
import TheHeader from "@/components/TheHeader.vue";
import EntryEditor from "./components/EntryEditor.vue";
import EntryCard from "@/components/EntryCard.vue";
import type User from "@/types/User";
import type Entry from "./types/Entry";
import { userInjectionKey } from "./injectionKeys";

const user = ref<User>({
  id: 1,
  username: "ashn",
  settings: [],
});

provide(userInjectionKey, user.value);

const entryList: Ref<Entry[]> = ref([]);

const handleCreateEntry = (entry: Entry) => {
  entryList.value.unshift(entry);
};
</script>

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
