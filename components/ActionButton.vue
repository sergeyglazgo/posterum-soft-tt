<template>
  <button
    class="px-[25px] h-14 bg-white rounded-2xl bg-opacity-10 hover:bg-opacity-20
    disabled:bg-opacity-10 disabled:opacity-60 transition"
    :disabled="disabled"
    @click="emitAction"
  >
    <slot />
  </button>
</template>

<script setup>
import { EActionType } from "../types"

const props = defineProps({
  disabled: {
    type: Boolean,
    default: false
  },
  actionType: String
})

const emit = defineEmits([...Object.values(EActionType)])

function emitAction() {
  switch (props.actionType) {
    case EActionType.OPEN:
      emit(EActionType.OPEN)
      break
    case EActionType.CLOSE:
      emit(EActionType.CLOSE)
      break
    case EActionType.NEXT:
      emit(EActionType.NEXT)
      break
    case EActionType.PREV:
      emit(EActionType.PREV)
      break
  }
}
</script>
