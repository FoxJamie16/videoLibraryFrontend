<template>
    <div backgroundcolor="light">
        <h3>Retrieve a video</h3>
      <input type="text" ref="textInput" @change="handleFileChange" />
      <button @click="getVideo">Get Video</button>
    </div>
  </template>
  
<script>
  import FileSaver from 'file-saver';
  const downloadVideo = (key) => {
    // Make a POST request to the backend endpoint for file upload
    fetch('http://localhost:3000/'+key, {
          method: 'get',
        })
          .then(async data => {
            console.log('Video retrieved successfully:', data);
            const blob = await data.blob();

            FileSaver.saveAs(blob, "test.mp4");
          })
          .catch(error => {
            console.error('Error uploading video:', error);
          });
  } 

  export default {
    data() {
      return {
        selectedFile: null
      };
    },
    mounted(){
        this.getFileFromURL();},
    methods: {
      handleFileChange(event) {
        this.selectedFile = event.target.value;
      },
      getVideo() {
        const formData = new FormData();
        formData.append('key', this.selectedFile);
        
        downloadVideo(this.selectedFile);
      },

      getFileFromURL(){
        if(((new URL(window.location.href)).pathname.split('/')[1])!=""){
            this.selectedFile = (new URL(window.location.href)).pathname.split('/')[1];
            downloadVideo(this.selectedFile);   
        }
      }
    }
  };
</script>