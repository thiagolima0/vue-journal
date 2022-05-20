<template>
  <form
    class="entry-form"
    @submit.prevent="
      $emit('@create', {
        id: Math.random(),
        userId: 1,
        body,
        emoji,
        createdAt: new Date(),
      })
    "
  >
    <textarea
      :value="body"
      @keyup="handleTextInput"
      placeholder="New Journal Entry for danielkelly_io"
    ></textarea>
    <EmojiField v-model="emoji" />
    <div class="entry-form-footer">
      <span>{{ chartCount }} / {{ maxChars }}</span>
      <button>Remember <ArrowCircleRight width="20" /></button>
    </div>
  </form>
</template>

<script lang="ts" setup>
import EmojiField from "@/components/EmojiField.vue";
import ArrowCircleRight from "@/assets/icons/arrow-circle-right.svg";
import type Emoji from "@/types/Emoji";
import { ref, computed } from "vue";
import type Entry from "@/types/Entry";

// data

const body = ref("");
const emoji = ref<Emoji | null>(null);
const chartCount = computed<number>(() => body.value.length);
const maxChars = 280;

// events

defineEmits<{
  (e: "@create", entry: Entry): void;
}>();

// methods

const handleTextInput = (e: Event) => {
  const textarea = e.target as HTMLTextAreaElement;

  if (body.value.length < maxChars) {
    body.value = textarea.value;
  } else {
    body.value = textarea.value = textarea.value.substring(0, maxChars);
  }
};
</script>
