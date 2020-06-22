<template>
  <div class="container">
    <div class="file-selector">
      <figure>
        <UploadIcon/>
      </figure>Select Files from Google Drive
      <p>
        <span>Authenticate with Google Drive</span>
      </p>
      <button type="button" @click="driveIconClicked();">Connect to Google Drive</button>
    </div>
    <AttachmentList :tempAttachments="getTempAttachments"/>
  </div>
</template>

<script>
import AttachmentList from "./AttachmentList";
import UploadIcon from "./UploadIcon";
export default {
  name: "Attachment",
  data() {
    return {
      tempAttachments: [],
      attachments: [],
      pickerApiLoaded: false,
      developerKey: " <-- YOUR API KEY --> ",
      clientId: "<-- YOUR OAUTH CLIENT ID --> ",
      scope: "https://www.googleapis.com/auth/drive.readonly",
      oauthToken: null
    };
  },
  components: {
    AttachmentList: AttachmentList,
    UploadIcon
  },
  mounted() {
    let gDrive = document.createElement("script");
    gDrive.setAttribute("type", "text/javascript");
    gDrive.setAttribute("src", "https://apis.google.com/js/api.js");
    document.head.appendChild(gDrive);
  },
  methods: {
    // function called on click of drive icon
    async driveIconClicked() {
      console.log("Clicked");
      await gapi.load("auth2", () => {
        console.log("Auth2 Loaded");
        gapi.auth2.authorize(
          {
            client_id: this.clientId,
            scope: this.scope,
            immediate: false
          },
          this.handleAuthResult
        );
      });
      gapi.load("picker", () => {
        console.log("Picker Loaded");
        this.pickerApiLoaded = true;
        this.createPicker();
      });
    },

    handleAuthResult(authResult) {
      console.log("Handle Auth result");
      if (authResult && !authResult.error) {
        this.oauthToken = authResult.access_token;
        this.createPicker();
      }
    },

    // Create and render a Picker object for picking user Photos.
    createPicker() {
      console.log("Create Picker");
      if (this.pickerApiLoaded && this.oauthToken) {
        var picker = new google.picker.PickerBuilder()
          .enableFeature(google.picker.Feature.MULTISELECT_ENABLED)
          .addView(google.picker.ViewId.DOCS)
          .setOAuthToken(this.oauthToken)
          .setDeveloperKey("AIzaSyBaQZlYTmndQYCcdlkHoVtBzpZYandwaaA")
          .setCallback(this.pickerCallback)
          .build();
        picker.setVisible(true);
      }
    },
    async pickerCallback(data) {
      console.log("PickerCallback Files : ", data);
      var url = "nothing";
      var name = "nothing";
      if (data[google.picker.Response.ACTION] === google.picker.Action.PICKED) {
        var doc = data[google.picker.Response.DOCUMENTS][0];
        url = doc[google.picker.Document.URL];
        name = doc.name;
        let docs = data.docs;
        var param = { fileId: doc.id, oAuthToken: this.oauthToken, name: name };
        let attachments = [];
        for (let i = 0; i < docs.length; i++) {
          let attachment = {};
          attachment._id = docs[i].id;
          attachment.title = docs[i].name;
          attachment.name = docs[i].name + "." + docs[i].mimeType.split("/")[1];
          attachment.type = "gDrive";
          attachment.description = "Shared with GDrive";
          attachment.extension =
            "." +
            docs[i].mimeType.substring(docs[i].mimeType.lastIndexOf(".") + 1);
          attachment.iconURL = docs[i].iconUrl;
          attachment.size = docs[i].sizeBytes;
          attachment.user = JSON.parse(localStorage.getItem("user"));
          attachment.thumb = null;
          attachment.thumb_list = null;
          attachments.push(attachment);
        }
        this.tempAttachments = [...attachments];
      }
      this.oauthToken = null;
      this.pickerApiLoaded = false;
    }
  },
  computed: {
    getTempAttachments() {
      return this.tempAttachments;
    },
    getAttachments() {
      return this.attachments;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.file-selector {
  padding: 55px;
  font-weight: 600;
  background-color: #f9f9f9;
  border: 1px solid #ccc;
  border-radius: 4px;
  color: #4e5b69;
  z-index: -9;
}
figure {
  margin: 0px;
}

.dropzone-container {
  display: flex;
  flex-direction: column;
  border: 1px dashed #ccc;
  border-radius: 15px;
}
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
button {
  background: #031629;
  box-shadow: 0 0 2px 0 rgba(3, 22, 41, 0.11),
    0 6px 16px 0 rgba(3, 22, 41, 0.08);
  font-family: SFProDisplay-Regular;
  font-size: 14px;
  color: #ffffff;
  letter-spacing: 0.4px;
  padding: 12px 30px;
  border-radius: 4px;
  outline: none;
  cursor: pointer;
  transition: all 0.25s;
}

button:hover {
  background-color: rgba(65, 184, 131, 1);
  border-color: transparent;
}
.separator {
  position: relative;
}
.separator:after {
  position: absolute;
  content: "";
  height: 1px;
  width: 200px;
  background: #d8d8d8;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
span {
  position: relative;
  background: #f9f9f9;
  padding: 0 4px;
  z-index: 9;
  font-size: 12px;
  color: #4e5b69;
}
</style>
