<template>
<div>
<Navbar />

<div class="container">
<div class="row">
<div class="col">
<div class="justify-content-center.align-self-center"><br><br>
<h2><strong>Project Tes, </strong><br>Fikri Rahmat Fauzi</h2>
<h4>Developed Aplication Vue, API, and Bootstrap</h4><br>
<img src="../assets/image/project.png" width="200" />
</div>
</div>
<div class="col">
<img src="../assets/image/hero.png" width="500" />
</div>
</div>
    <ImageUploader />
    </div>
</div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import ImageUploader from '@/components/Image.vue'



export default {
  name: 'Image',
  components: {
    Navbar,
    ImageUploader,
    
  }
}

</script>
<style>
</style>