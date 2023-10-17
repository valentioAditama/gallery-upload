<template>
  <!-- Main modal -->
  <div
    id="defaultModal"
    tabindex="-1"
    aria-hidden="true"
    class="fixed top-0 left-0 right-0 z-50 hidden w-full p-4 overflow-x-hidden overflow-y-auto md:inset-0 h-[calc(100%-1rem)] max-h-full"
  >
    <div class="relative w-full max-w-2xl max-h-full">
      <!-- Modal content -->
      <div class="relative bg-white rounded-lg shadow dark:bg-gray-700">
        <!-- Modal header -->
        <div class="flex items-start justify-between p-4 border-b rounded-t dark:border-gray-600">
          <h3 class="text-xl font-semibold text-gray-900 dark:text-white">Upload your images</h3>
          <button
            type="button"
            class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm w-8 h-8 ml-auto inline-flex justify-center items-center dark:hover:bg-gray-600 dark:hover:text-white"
            data-modal-hide="defaultModal"
          >
            <svg
              class="w-3 h-3"
              aria-hidden="true"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 14 14"
            >
              <path
                stroke="currentColor"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="m1 1 6 6m0 0 6 6M7 7l6-6M7 7l-6 6"
              />
            </svg>
            <span class="sr-only">Close modal</span>
          </button>
        </div>
        <!-- Modal body -->
        <div class="p-6 space-y-6">
          <div class="flex items-center justify-center w-full">
            <label
              for="dropzone-file"
              class="flex flex-col items-center justify-center w-full h-64 border-2 border-gray-300 border-dashed rounded-lg cursor-pointer bg-gray-50 dark:hover:bg-bray-800 dark:bg-gray-700 hover:bg-gray-100 dark:border-gray-600 dark:hover:border-gray-500 dark:hover:bg-gray-600"
            >
              <div class="flex flex-col items-center justify-center pt-5 pb-6">
                <svg
                  class="w-8 h-8 mb-4 text-gray-500 dark:text-gray-400"
                  aria-hidden="true"
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 20 16"
                >
                  <path
                    stroke="currentColor"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M13 13h3a3 3 0 0 0 0-6h-.025A5.56 5.56 0 0 0 16 6.5 5.5 5.5 0 0 0 5.207 5.021C5.137 5.017 5.071 5 5 5a4 4 0 0 0 0 8h2.167M10 15V6m0 0L8 8m2-2 2 2"
                  />
                </svg>
                <p class="mb-2 text-sm text-gray-500 dark:text-gray-400">
                  <span class="font-semibold">Click to upload</span>
                </p>
                <p class="text-xs text-gray-500 dark:text-gray-400">
                  .JPG, .JPEG, .BMP, .PNG, or .GIF (MAX SIZE: 2048KB)
                </p>
              </div>
              <input
                id="dropzone-file"
                type="file"
                @change="onFileChange"
                ref="imageInput"
                class="hidden"
                required
                accept=".jpg, .jpeg, .bmp, .png, .gif"
              />
            </label>
          </div>
          <div class="mt-4" v-if="selectedImage">
            <img :src="selectedImage" alt="Selected Image" class="w-full h-full" />
          </div>
        </div>
        <!-- Modal footer -->
        <div
          class="flex items-center p-6 space-x-2 border-t border-gray-200 rounded-b dark:border-gray-600"
        >
          <button
            type="button"
            @click="handleSubmit"
            :disabled="isLoading"
            class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
          >
            <button
              disabled
              v-if="isLoading"
              type="button"
              class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800 inline-flex items-center"
            >
              <svg
                aria-hidden="true"
                role="status"
                class="inline w-4 h-4 mr-3 text-white animate-spin"
                viewBox="0 0 100 101"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z"
                  fill="#E5E7EB"
                />
                <path
                  d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z"
                  fill="currentColor"
                />
              </svg>
              Loading...
            </button>
            <span v-else>Upload</span>
          </button>
          <button
            data-modal-hide="defaultModal"
            type="button"
            class="text-gray-500 bg-white hover:bg-gray-100 focus:ring-4 focus:outline-none focus:ring-blue-300 rounded-lg border border-gray-200 text-sm font-medium px-5 py-2.5 hover:text-gray-900 focus:z-10 dark:bg-gray-700 dark:text-gray-300 dark:border-gray-500 dark:hover:text-white dark:hover:bg-gray-600 dark:focus:ring-gray-600"
          >
            Close
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Swal from 'sweetalert2'

export default {
  name: 'imageInput',
  data() {
    return {
      image: null,
      selectedImage: null,
      isLoading: false // track loading status
    }
  },
  methods: {
    // display image after upload to the form
    onFileChange(event) {
      const file = event.target.files[0]
      if (file) {
        const reader = new FileReader()
        reader.onload = (e) => {
          this.selectedImage = e.target.result
        }
        reader.readAsDataURL(file)
      } else {
        this.selectedImage = null
      }
    },
    handleSubmit() {
      // set loading state to true
      this.isLoading = true

      // Get image from input
      const imageInput = this.$refs.imageInput.files[0]

      // Check extension allowed
      const fileExtension = imageInput.name.split('.').pop().toLowerCase()
      const allowedExtension = ['jpg', 'jpeg', 'bmp', 'png', 'gif']

      // Check if the extension is allowed
      if (!allowedExtension.includes(fileExtension)) {
        Swal.fire({
          icon: 'error',
          title: 'Error',
          text: 'Hanya boleh file gambar dengan ekstensi jpg, jpeg, bmp, png, atau gif'
        })
        this.isLoading = false
        return // Terminate the function
      }

      // Create FormData object to store an image file
      const formData = new FormData()
      formData.append('image', imageInput)

      // Create a POST request to the ImgBB API
      axios
        .post(
          'https://api.imgbb.com/1/upload?expiration=600&key=e12749a9f582007d6f83f05bf97b1a38',
          formData
        )
        .then((response) => {
          // Handle the response from the API and display an alert
          console.log(response)
          // check maxSize images
          const fileSizeInKB = imageInput.size / 1024 // convert to kb
          if (fileSizeInKB > 2048) {
            Swal.fire({
              icon: 'error',
              title: 'error',
              text: 'File gambar terlalu besar (Maksimal 2048 KB)'
            })
            this.isLoading = false
            return // Terminate the function
          } else if (response.data.status === 200) {
            Swal.fire({
              icon: 'success',
              title: 'Success',
              text: 'Gambar berhasil diupload'
            })
            // Store in localStorage
            const uploadedImages = JSON.parse(localStorage.getItem('uploadImages')) || []
            uploadedImages.push(response.data.data.url)
            localStorage.setItem('uploadImages', JSON.stringify(uploadedImages))
          } else {
            Swal.fire({
              icon: 'error',
              title: 'Error',
              text: 'Upload Error'
            })
          }
        })
        .catch((err) => {
          // Handle the error response from the API and display an alert
          console.log(err)
          if (err.response && err.response.status === 400) {
            Swal.fire({
              icon: 'error',
              title: 'Error',
              text: 'Hanya boleh file gambar dan tidak boleh kosong'
            })
          } else if (err.response && err.response.status === 413) {
            Swal.fire({
              icon: 'error',
              title: 'Error',
              text: 'File Gambar terlalu besar'
            })
          }
        })
        .finally(() => {
          this.isLoading = false // Set Loading to false
          document.getElementById('defaultModal').classList.add('hidden-modal')
          this.selectedImage = null // clean image from onchange
          // auto refresh after uploaded
          setTimeout(() => {
            window.location.reload()
          }, 3000)
        })
    }
  }
}
</script>
