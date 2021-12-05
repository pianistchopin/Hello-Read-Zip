<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">

   <input type="file" @change="loadTextFromFile">
  </div>


</template>

<script>
import JSZip from 'jszip';

export default {
  data(){
    return{
      new_zip: undefined,
      text: "",
      ff:undefined
    }
  },
  name: 'App',
  components: {
  },

   mounted() {
    this.getData()
  },

  methods:{

    getData(){

    },

    loadTextFromFile(event){
      this.new_zip = new JSZip();

      this.ff = event.target.files;
      for(var i = 0; i < this.ff.length; i++){
        this.new_zip.loadAsync(this.ff[i]).then(function(zip){
          zip.forEach(function(relativePath, zipEntry){
            console.log(zipEntry.name);
          });

           return zip.file("hello.txt").async("string");
        }).then(function(text){
          console.log(text);
        })
      }
    }
  }
}
</script>

