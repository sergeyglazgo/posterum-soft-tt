<template>
  <div v-if="showModal" class="fixed inset-0 flex flex-col items-center justify-center bg-[#0d0d0d] bg-opacity-90">
    <ActionButton
      class="absolute top-12 right-12 flex"
      :action-type="EActionType.CLOSE"
      @close="$emit(EActionType.CLOSE)"
    >
      <template #default>
        <img
          src="../static/icons/cross.svg"
          alt="close modal icon"
          class="inline m-auto w-2"
        />
      </template>
    </ActionButton>

    <div class="flex items-center">
      <ActionButton
        class="flex"
        :action-type="EActionType.PREV"
        :disabled="currentIndex === 0"
        @prev="prevPic"
      >
        <template #default>
          <img
            src="../static/icons/arrowleft.svg"
            alt="previous"
            class="inline m-auto"
          />
        </template>
      </ActionButton>

      <div class="max-w-lg mx-6 mb-4 text-white">
        <div class="flex justify-between text-3xl mb-3">
          <span>Kor Blockchain Badge</span>
          <span>#{{ currentPic.id }}</span>
        </div>
        <div class="flex gap-6 mb-4">
          <a href="#" @click.prevent>
            <img
              src="../static/icons/owner.svg"
              alt="owner icon"
              class="inline pr-2 opacity-40"
            />
            <span class="underline">Owner</span>
          </a>
          <a href="#" @click.prevent>
            <img
              src="../static/icons/collection.svg"
              alt="collection icon"
              class="inline pr-2 opacity-40"
            />
            <span class="underline">Collection</span>
          </a>
          <button @click="copyUrl">
            <img
              src="../static/icons/share.svg"
              alt="share icon"
              class="inline pr-2"
            />
            <span class="underline">Share</span>
          </button>
        </div>
        <img :src="currentPic.imageUrl" class="w-full rounded-[17px]" />
      </div>

      <ActionButton
        class="flex"
        :action-type="EActionType.NEXT"
        :disabled="currentIndex === pictures.length - 1"
        @next="nextPic"
      >
        <template #default>
          <img
            src="../static/icons/arrowright.svg"
            alt="next"
            class="inline m-auto"
          />
        </template>
      </ActionButton>
    </div>

    <ActionButton
      class="px-8 text-white text-sm"
      :action-type="EActionType.OPEN"
      disabled
      @next="nextPic"
    >
      <template #default>
        OPEN MARKETPLACE
      </template>
    </ActionButton>
  </div>
</template>

<script setup>
import { computed, ref, watch } from "vue"
import { EActionType } from "../types"

const props = defineProps({
  showModal: Boolean,
  pictures: Array,
  index: Number
})

defineEmits(['close'])

const currentIndex = ref(props.index)
const currentPic = computed(() => props.pictures[currentIndex.value])

function nextPic() {
  if (currentIndex.value < props.pictures.length - 1) {
    currentIndex.value++
  }
}

function prevPic() {
  if (currentIndex.value > 0) {
    currentIndex.value--
  }
}

function copyUrl() {
  const url = window.location.href
  navigator.clipboard.writeText(url)
}

watch(() => props.index, (newVal) => {
  currentIndex.value = newVal
})
</script>
