<template>
    <div>
      <h3>Upload a video
      </h3>
      <input type="file" ref="fileInput" @change="handleFileUpload" accept="video/*" />
      <button @click="uploadVideo">Upload Video</button>
      <h3 v-if="id">Upload success! Video id: {{id}}. Share by typing id below or appending "/id" onto url. </h3>
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
      handleFileUpload(event) {
        this.selectedFile = event.target.files[0];
      },
      uploadVideo() {
        const formData = new FormData();
        formData.append('video', this.selectedFile);
        //formData.append('id', '123456');
  
        // Make a POST request to the backend endpoint for file upload
        fetch('https://video-library-backend-fort.vercel.app/upload', {
          method: 'POST',
          body: formData
        })
          .then(response => response.json())
          .then(data => {
            // Handle the response from the backend
            let array = data.url.split("/");
            let id =  array[array.length-1];
            this.id = id
          })
          .catch(error => {
            console.error('Error uploading video:', error);
            // Handle the error case
          });
      }
    }
  };
</script>
