<template>
<div>
 <H2>Masukan Gambar</H2><br>
 <input type="file" ref="fileInput" @change="handleFileChange" accept="image/*" />
    <button @click="uploadImage">Upload</button>
    <div>{{ statusMessage }}</div><br>
    <div class="image-gallery">
      <img v-for="url in imageUrls" :key="url" :src="url" alt="Gambar" />
    </div>
    <br>
    <br>
    <h5>Copyright &copy; Fikri Rahmat Fauzi | 2023</h5>
 </div>
</template>

<script>
import axios from "axios";
export default {
    data() {
    return {
      selectedFile: null,
      statusMessage: "",
      imageUrls: [],
    };
  },
    methods: {
    handleFileChange(event) {
      this.selectedFile = event.target.files[0];
    },
    uploadImage() {
      if (!this.selectedFile) {
        this.statusMessage = "Pilih gambar terlebih dahulu.";
        return;
      }

      // Validasi ekstensi file
      const allowedExtensions = ["jpg", "jpeg", "bmp", "png", "gif"];
      const fileExtension = this.selectedFile.name.split(".").pop().toLowerCase();

      if (!allowedExtensions.includes(fileExtension)) {
        this.statusMessage = "Hanya diperbolehkan file gambar.";
        return;
      }

      // Validasi ukuran file
      if (this.selectedFile.size > 2 * 1024 * 1024) {
        this.statusMessage = "File gambar terlalu besar (maksimal 2MB).";
        return;
      }

      const formData = new FormData();
      formData.append("image", this.selectedFile);

      // Ganti 'YOUR_API_KEY' dengan API key imgBB Anda
      const apiKey = "517b68aee3c0923a68049c26c9796eb1";
      axios
        .post(`https://api.imgbb.com/1/upload?key=${apiKey}`, formData)
        .then((response) => {
          this.statusMessage = "Gambar berhasil diupload.";
          this.imageUrls.push(response.data.data.url);

          // Simpan daftar URL gambar di LocalStorage
          localStorage.setItem("imageUrls", JSON.stringify(this.imageUrls));
        })
        .catch((error) => {
          this.statusMessage = "Upload error.";
          console.error(error);
        });
    },
  },
  mounted() {
    // Ambil daftar URL gambar dari LocalStorage saat halaman dimuat
    const savedImageUrls = localStorage.getItem("imageUrls");
    if (savedImageUrls) {
      this.imageUrls = JSON.parse(savedImageUrls);
    }
  },
name : 'ImageUploader'

}

</script>

<style>
.image-gallery {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}
.image-gallery img {
  max-width: 300px;
  height: auto;
}
button {
  background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}
</style>
