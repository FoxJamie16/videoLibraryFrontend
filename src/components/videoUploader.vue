<template>
    <div>
      <h3>Upload a video
      </h3>
      <input type="file" ref="fileInput" @change="handleFileChange" accept="video/*" />
      <button @click="uploadVideo">Upload Video (MP4)</button>
      <h3 v-if="id">Upload success! Video id: {{id}}. Download by typing id below or appending "/id" onto url. </h3>
    </div>
  </template>
  
<script>
  export default {
    data() {
      return {
        selectedFile: null,
        id: ""
      };
    },
    methods: {
      handleFileChange(event) {
        this.selectedFile = event.target.files[0];
      },
      uploadVideo() {
        const formData = new FormData();
        formData.append('video', this.selectedFile);
  
        // Make a POST request to the backend endpoint for file upload
        fetch('https://video-library-backend-fort.vercel.app/upload', {
          method: 'POST',
          body: formData
        })
          .then(response => response.json())
          .then(data => {
            // Retrieves video id from api reponse, passes it into Vue message for user. 
            let array = data.url.split("/");
            let id =  array[array.length-1];
            this.id = id
          })
          .catch(error => {
            console.error('Error uploading video:', error);
          });
      }
    }
  };
</script>
