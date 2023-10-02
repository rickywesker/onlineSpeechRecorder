<template>
  <div class="hello">
    <h1>Read the text ({{index}}/{{total}})</h1>
    <h3>{{text}}</h3>
    <br>

    <div style="width: 400px; margin: auto; text-align: center;">
      <audio-recorder :pause-recording="callback" :after-recording="callback"/>
      <br>
      <audio v-if="url" :src="url" controls :title="file_name"/>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  props: {
    text: String,
    index: Number,
    total: Number
  },
  data() {
    return {
      recording: false,
      url: null
    };
  },
  computed: {
    file_name() {
      let padded_number = "";
      if (this.index < 10) {
        padded_number = `00${this.index + 1}`;
      } else if (this.index < 100) {
        padded_number = `0${this.index + 1}`;
      } else {
        padded_number = `${this.index + 1}`;
      }

      return `utterance-${padded_number}.mp3`;
    }
  },
  methods: {
    toggle_record() {
      this.recording = !this.recording;
    },
    callback(data) {
      console.debug(data);
      if (data && data.url) {
        this.url = data.url; // window.URL.createObjectURL(data.blob);
        // Upload the audio file to the server
        const formData = new FormData();
        formData.append('audio', data.blob, `voice_${this.index}.mp3`);
        
        axios.post('http://localhost:5000/upload', formData, {
            headers: {
                'Content-Type': 'multipart/form-data'
            }
        })
        .then(response => {
            console.log('Upload successful:', response.data);
        })
        .catch(error => {
            console.error('Upload error:', error);
        });
        // var link = document.createElement("a");
        // link.href = this.url;
        // link.innerHTML = "download here";
        // link.download = `voice_${this.index}.mp3`;
        // // link.style = "display: none";
        // document.body.appendChild(link);
        // link.click();
        // console.log("dine");
        // window.URL.revokeObjectURL(this.url);
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
h3 {
  margin: 40px 0 0;
}

.ar-records {
  display: none !important;
}

.ar-player {
  display: none !important;
}
</style>
