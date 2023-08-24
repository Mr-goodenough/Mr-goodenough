<template>
    <div>
      <input type="file" ref="fileInput" @change="handleFileChange" >
      <button @click="uploadFile">上传文件</button>
    </div>
</template>
  
<script lang='js'>
  import { ref } from 'vue';
  import axios from 'axios';
  
  export default {
    setup() {
      const selectedFile = ref(null);
      const fileInputRef = ref(null);
  
      const handleFileChange = (event) => {
        selectedFile.value = event.target.files[0];
      };
  
      const uploadFile = async () => {
        if (!selectedFile.value) {
          alert("请选择一个文件");
          return;
        }
  
        const formData = new FormData();
        formData.append("file", selectedFile.value);
  
        try {
          const response = await axios.post("http://localhost:8080/pictures", formData, {
            headers: {
              "Content-Type": "multipart/form-data",
            },
          });
  
          if (response.status === 200) {
            alert("文件上传成功");
          } else {
            alert("文件上传失败");
          }
        } catch (error) {
          console.error("上传过程出错:", error);
        }
      };
  
      return {
        selectedFile,
        handleFileChange,
        uploadFile,
      };
    },
  };
  </script>
  
  
