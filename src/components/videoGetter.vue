<template>
    <div backgroundcolor="light">
        <h3>Retrieve a video</h3>
      <input type="text" ref="textInput" @change="handleFileChange" />
      <button @click="getVideo">Get Video</button>
      <!--To improve usability, a v-if combined with an 'uploadSuccess' variable could be
         included to show a download button instead of immediately starting the download --> 
    </div>
  </template>
  
<script>
  import FileSaver from 'file-saver';
  const downloadVideo = (key) => {
    // Make a GET request to the backend endpoint for file download
    fetch('https://video-library-backend-fort.vercel.app/'+key, {
          method: 'get',
        })
          .then(async data => {
            // Video retrieved  successfully
            const blob = await data.blob();

            FileSaver.saveAs(blob, "video.mp4");
          })
          .catch(error => {
            console.error('Error downloading video:', error);
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
      
      // Allows retrieving of video by following a given link, a more robust solution would be provided by vue router. 
      getFileFromURL(){
        if(((new URL(window.location.href)).pathname.split('/')[1])!=""){
            this.selectedFile = (new URL(window.location.href)).pathname.split('/')[1];
            downloadVideo(this.selectedFile);   
        }
      }
    }
  };
</script>
