<template>
  <div>
    <ul v-if="tempAttachments.length > 0">
      <li v-for="tempAttachment in tempAttachments" :key="tempAttachment._id">
        <div class="file-details">
          <div class="file-name display-flex align-center">
            <p class="" ref="attachmentTitle">{{ tempAttachment.title }}</p>
          </div>
          <div class="file-info">
            <span class="uploaded-date"> {{ tempAttachment.size }} bytes </span>
            <span v-if="checkProgress(tempAttachment)" class="upload-prgress">
              {{ `${tempAttachment.progress} %` }}
            </span>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "AttachmentList",
  methods: {
    checkProgress(attachment) {
      return attachment.progress === null ? false : true;
    }
  },
  props: {
    tempAttachments: {
      type: Array
    },
    attachments: {
      type: Array
    }
  }
};
</script>

<style>
ul {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
  padding: 0px;
}
li {
  border: 1px solid;
  margin-bottom: 8px;
  border-radius: 8px;
  margin-right: 8px;
  padding: 0 10px;
}
.file-name {
  min-width: 150px;
  font-size: 13px;
}
.uploaded-date {
  font-size: 12px;
}
.upload-progress {
  font-size: 12px;
}
.file-info {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}
</style>
