<template>
  <BubbleMenu
    v-if="bubbleMenuButtons"
    class="bubble-menu rounded-md shadow-sm"
    :tippy-options="{ duration: 100 }"
    :editor="editor"
    v-bind="options"
  >
    <Menu
      class="rounded-md border-gray-100 shadow-lg"
      :buttons="bubbleMenuButtons"
    />
  </BubbleMenu>
</template>
<script>
import { BubbleMenu } from '@tiptap/vue-3'
import { createEditorButton } from './utils'
import Menu from './Menu.vue'

export default {
  name: 'TextEditorBubbleMenu',
  props: ['buttons', 'options'],
  components: { BubbleMenu, Menu },
  inject: ['editor'],
  computed: {
    bubbleMenuButtons() {
      if (!this.buttons) return false

      let buttons
      if (Array.isArray(this.buttons)) {
        buttons = this.buttons
      } else {
        buttons = [
          'Paragraph',
          'Heading 2',
          'Heading 3',
          'Separator',
          'Bold',
          'Italic',
          'Strikethrough',
          'FontColor',
          'Link',
          'Separator',
          'Bullet List',
          'Numbered List',
          'Task List',
          'Separator',
          'Align Left',
          'Align Center',
          'Align Right',
          'Separator',
          'Image',
          'Video',
          'Blockquote',
          'Code',
          [
            'InsertTable',
            'AddColumnBefore',
            'AddColumnAfter',
            'DeleteColumn',
            'AddRowBefore',
            'AddRowAfter',
            'DeleteRow',
            'MergeCells',
            'SplitCell',
            'ToggleHeaderColumn',
            'ToggleHeaderRow',
            'ToggleHeaderCell',
            'DeleteTable',
          ],
        ]
      }
      return buttons.map(createEditorButton)
    },
  },
}
</script>
