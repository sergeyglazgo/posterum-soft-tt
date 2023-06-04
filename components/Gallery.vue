<template>
  <div class="flex flex-wrap justify-center gap-3">
    <div v-for="(pic, index) in pictures" :key="pic.id">
      <img
        :src="pic.imageUrl"
        class="cursor-pointer rounded max-w-[250px]"
        @click="openModal(index)"
      />
    </div>
  </div>
  <ModalPicViewer
    :show-modal="showModal"
    :pictures="pictures"
    :index="currentIndex"
    @close="closeModal"
  />
</template>

<script setup>
import { ref, onMounted } from 'vue'
import data from '../static/pictures'

const pictures = ref(JSON.parse(data))

const showModal = ref(false)
const currentIndex = ref(0)


function openModal(index) {
  currentIndex.value = index
  showModal.value = true
  document.body.style.overflow = 'hidden'
}

function closeModal() {
  showModal.value = false
  document.body.style.overflow = ''
}

onMounted(() => {
  document.body.style.overflow = ''
});
</script>

