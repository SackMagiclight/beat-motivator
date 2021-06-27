<template>
  <div
    class="flex items-center justify-center w-full h-32 text-center"
    id="app"
  >
    <div
      class="w-full h-full bg-gray-100 border border-dashed border-gray-300"
      @dragover="dragover"
      @dragleave="dragleave"
      @drop="drop"
    >
      <input
        type="file"
        ref="fileRef"
        id="assetsFieldHandle"
        class="hidden opacity-0 overflow-hidden"
        @change="onChange"
        accept=".csv"
      />

      <label
        for="assetsFieldHandle"
        class="cursor-pointer h-full flex items-center justify-center"
      >
        <div>
          ここにファイルをドラッグアンドドロップするか、クリックしてファイルを選択します。
        </div>
      </label>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from '@nuxtjs/composition-api'

export default defineComponent({
  props: {
    file: {
      default: null,
    },
  },

  setup(props, context) {
    const fileRef = ref<HTMLInputElement | null>(null)

    const onChange = () => {
      context.emit(
        'update:file',
        fileRef.value?.files ? fileRef.value?.files.item(0) : null
      )
    }

    const dragover = (event: DragEvent) => {
      event.preventDefault()
    }

    const dragleave = (event: DragEvent) => {
      event.preventDefault()
    }

    const drop = (event: DragEvent) => {
      event.preventDefault()
      context.emit(
        'update:file',
        event.dataTransfer?.files ? event.dataTransfer?.files.item(0) : null
      )
    }

    return {
      fileRef,
      onChange,
      dragover,
      dragleave,
      drop,
    }
  },
})
</script>
