<template>
  <div class="container">
    <h2 align="center">Workshop #2 - Preview Image</h2>
    <hr />
    <div v-if="!image">
      <input type="file" class="form-control" @change="onFileChange" />
      <hr />
    </div>
    <div v-else>
      <img :src="image" class="img-fluid" />
      <hr />
      <button class="btn btn-danger" @click="removeImage">Remove</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      image: "",
    };
  },
  methods: {
    onFileChange: function (e) {
      var files = e.target.files;
      if (!files.length) return;
      this.createImage(files[0]);
    },
    createImage(files) {
      var reader = new FileReader();
      reader.onload = (e) => {
        this.image = e.target.result;
      };
      reader.readAsDataURL(files);
    },
    removeImage() {
      this.image = "";
    },
  },
};
</script>
