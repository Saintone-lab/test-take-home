<template>
  <div class="container">
    <div class="row mt-4">
      <div class="col-lg-8">
        <div class="header d-flex">
          <div class="search d-flex position-relative align-items-center">
            <input type="text" class="search__input" placeholder="Search...">
            <div class="search__icon">
              <i class="fi fi-br-search"></i>
            </div>
          </div>
          <div class="filter m-2">
            <a href="#" class="btn btn-light btn-filter d-flex align-items-center justify-content-center">
              <i class="fi fi-sr-settings-sliders"></i>
            </a>
          </div>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-sm-4 col-lg-2">
        <div class="card" style="width: 12rem;">
          <div id="drop-area">
            <form class="my-form">
              <input type="file" id="fileElem" multiple accept="image/*" @change="fileSelected" hidden>
              <label class="button" for="fileElem">Click Here to Upload Image</label>
              <div class="card-foot">
                <button class="btn btn-primary w-100" id="upFile" @click="onUpload">Upload</button>
              </div>
            </form>
          </div>
        </div>
      </div>
      <div v-for="(image) in dataImage" :key="image" class="col-sm-4 col-lg-2" >
        <div class="card" style="width: 12rem;">
          <img :src="image" id="gallery" class="card-img-top" alt="...">
        </div>
      </div>
      <div class="col-sm-4 col-lg-2">
        <div class="card" style="width: 12rem;">
          <img src="../assets/camp1.jpg" id="gallery2" class="card-img-top" alt="...">
        </div>
      </div>
      <div class="col-sm-4 col-lg-2">
        <div class="card" style="width: 12rem;">
          <img src="../assets/camp1.jpg" id="gallery3" class="card-img-top" alt="...">
        </div>
      </div>
      <div class="col-sm-4 col-lg-2">
        <div class="card" style="width: 12rem;">
          <img src="../assets/camp1.jpg" id="gallery4" class="card-img-top" alt="...">
        </div>
      </div>
      <div class="col-sm-4 col-lg-2">
        <div class="card" style="width: 12rem;">
          <img src="../assets/camp1.jpg" id="gallery5" class="card-img-top" alt="...">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Swal from 'sweetalert2'

export default {
  name: 'HomeView',
  
  data(){
    return{
      selectedFile : null,
      // dataImage : [],
      image : '',
      upFileBtn :  document.getElementById('upFile'),
    }
  },
  mounted() {
    // console.log(this.dataImage[1])
    if (localStorage.getItem('img')) {
      try {
        this.dataImage = JSON.parse(localStorage.getItem('img'));
      } catch(e) {
        localStorage.removeItem('img');
      }
    }
  },
  methods:{
    fileSelected(e){
      this.selectedFile = e.target.files[0]
      this.image = localStorage.getItem('img')
      console.log(URL.createObjectURL(this.selectedFile))
    },
    buttonDisabled(){
      if ( !this.selectedFile ) {
        this.upFile.class = "disabled"
      }
    },
    onUpload(){
      Swal.fire({
        title: 'Do you want to save the Images?',
        imageUrl: URL.createObjectURL(this.selectedFile),
        showDenyButton: true,
        confirmButtonText: 'Save',
        denyButtonText: `cancel`,
      }).then((result) => {
        if (result.isConfirmed && this.selectedFile.size < 2048 * 2048 && this.selectedFile.type == `image/png` || `image/gif` || `image/jpeg` || `image/jpg`) {
          const fd = new FormData();
          fd.append('image', this.selectedFile, this.selectedFile.name)
          axios.post('https://api.imgbb.com/1/upload?key=fa2a98251cb24d036c79e5bf08913d4c', fd)
          .then(res => {
          console.log(res.data.data)
          if(res.data){
            const parsedImg = JSON.stringify(res.data.data.display_url)
            console.log(parsedImg)
            localStorage.setItem('img', parsedImg)
            // const parsedDataImg = JSON.parse(this.image)
            // console.log(parsedDataImg)
            // this.dataImage.push[parsedDataImg]
          }
          })
          console.log(this.image)
          Swal.fire('Saved!', '', 'success')
        }else if (result.isConfirmed && this.selectedFile.size > 2048 * 2048 && this.selectedFile.type == `image/png` || `image/gif` || `image/jpeg` || `image/jpg`){
          Swal.fire('File is too Big (Max 2MB)', '', 'info')
        }else if (result.isConfirmed && this.selectedFile.size < 2048 * 2048 && this.selectedFile.type != `image/png` || `image/gif` || `image/jpeg` || `image/jpg`){
          Swal.fire('Image Requirement', '', 'info')
        } else if (result.isDenied) {
          Swal.fire('Changes are not saved', '', 'info')
        }
      })
    }
  }
}
</script>

<style scoped>
  .search__input {
    width: 20.4rem;
    height: 3.8rem;
    border: none;
    border-radius: 1rem;
    font-size: 1.2rem;
    padding-left: 3.8rem;
    box-shadow: inner-shadow;
    background: ghostwhite;
    font-family: inherit;
    color: var(--greyDark);
  }

  .search__input::placeholder { color: grey; }

  .search__input:focus { 
    outline: none; 
    box-shadow: shadow; 
  }
  .search__input:focus.search__icon {
    color: var(--primary);
  }
  .search__icon {
    height: 2rem;
    position: absolute;
    font-size: 1.6rem;
    padding: 0 1rem;
    display: flex;
    color: var(--greyDark);
    transition: .3s ease;
  }
  .btn{
    width: 4rem;
    height: 3.8rem;
  }
</style>
