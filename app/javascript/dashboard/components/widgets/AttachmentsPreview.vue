<template>
  <div>
    <div
      v-for="(attachment, index) in attachments"
      :key="attachment.id"
      class="preview-item"
    >
      <div class="thumb-wrap">
        <img
          v-if="isTypeImage(attachment.resource.type)"
          class="image-thumb"
          :src="attachment.thumb"
        />
        <span v-else class="attachment-thumb">
          📄
        </span>
      </div>
      <div class="file-name-wrap">
        <span class="item">
          {{ attachment.resource.name }}
        </span>
      </div>
      <div class="file-size-wrap">
        <span class="item">
          {{ formatFileSize(attachment.resource.size) }}
        </span>
      </div>
      <div class="remove-file-wrap">
        <button
          class="remove--attachment"
          @click="() => onRemoveAttachment(index)"
        >
          <i class="ion-android-close"></i>
        </button>
      </div>
    </div>
  </div>
</template>
<script>
import { formatBytes } from 'dashboard/helper/files';

export default {
  props: {
    attachments: {
      type: Array,
      default: () => [],
    },
    removeAttachment: {
      type: Function,
      default: () => {},
    },
  },
  methods: {
    onRemoveAttachment(index) {
      this.removeAttachment(index);
    },
    formatFileSize(size) {
      return formatBytes(size, 0);
    },
    isTypeImage(type) {
      return type.includes('image');
    },
  },
};
</script>
<style lang="scss" scoped>
.preview-item {
  display: flex;
  padding: 0 var(--space-small) var(--space-smaller);
}

.thumb-wrap {
  max-width: var(--space-jumbo);
  flex-shrink: 0;
  width: var(--space-medium);
  display: flex;
  align-items: center;
}

.image-thumb {
  width: var(--space-medium);
  height: var(--space-medium);
  object-fit: cover;
  border-radius: var(--border-radius-small);
}

.attachment-thumb {
  width: var(--space-medium);
  height: var(--space-medium);
  font-size: var(--font-size-medium);
  text-align: center;
}

.file-name-wrap,
.file-size-wrap {
  display: flex;
  align-items: center;
  padding: 0 var(--space-one);

  > .item {
    margin: 0;
    font-size: var(--font-size-mini);
    font-weight: var(--font-weight-medium);
  }
}

.preview-header {
  padding: var(--space-slab) var(--space-slab) 0 var(--space-slab);
}

.file-name-wrap {
  width: 100%;
}

.file-size-wrap {
  width: 20%;
  justify-content: flex-end;
}

.remove-file-wrap {
  display: flex;
  align-items: center;
  justify-content: center;
}

.remove--attachment {
  width: var(--space-medium);
  height: var(--space-medium);
  border-radius: var(--space-medium);
  font-size: var(--font-size-small);
  cursor: pointer;

  &:hover {
    background: var(--color-background);
  }
}
</style>
