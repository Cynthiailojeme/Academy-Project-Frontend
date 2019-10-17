<template>
  <div class="create">
    <div class="wrap">
      <div class="row" style="max-width:1350px;">
        <div class="col-md-3">
          <AdminSidebar />
        </div>

        <div class="col-md-9">
          <div class="otherSide">
            <div class="first">
              <p>Create Application</p>
            </div>
            <div class="apply">
              <form @submit.prevent="sendFile">
                <div class="form-row">
                  <div class="form-group col-md-6">
                    <div v-if="!applicants.image">
                      <input @click="clicked" class="first_box form-control" id="dotted" />
                      <i class="visible">
                        <img @click="clicked" src="../assets/plus.png" />
                        <span>&nbsp; &nbsp; Upload image</span>
                      </i>
                    </div>
                    <div v-else>
                      <img :src="applicants.image" class="fileimg" />
                      <input type="file" name="image" style="display:none" />
                      <button class="btn3" @click="removeImage">Remove image</button>
                    </div>
                    <!-- <div class="files" v-if="!image"> -->
                    <!-- <input

@click="clicked"
class="first_box form-control"
id="dotted"
/>
<i class="visible">
<img src="../assets/plus.png" @click="clicked" />
<span>&nbsp; &nbsp; Choose File</span>
                    </i>-->
                    <!-- </div> -->
                    <!-- <div v-else>
<img :src="image" class="fileimg" />
<input type="file" name="image" style="display:none" />
<button class="btn3" @click="removeImage">Remove image</button>
                    </div>-->
                  </div>
                  <div class="form-group col-md-6 pl-5">
                    <label class="batch">Link</label>
                    <input v-model="applicants.link" class="second_box2 form-control" />
                  </div>
                </div>
                <div class="form-row pt-4">
                  <div class="form-group col-md-6">
                    <label class="batch">Application closure date</label>
                    <input
                      v-model="applicants.application_date"
                      type="date"
                      class="second_box form-control"
                      placeholder="dd/mm/yyyy"
                    />
                  </div>
                  <div class="form-group col-md-6 pl-5">
                    <label class="batch">Batch ID</label>
                    <input
                      v-model="applicants.batch_id"
                      type="text"
                      class="second_box form-control"
                    />
                  </div>
                </div>
                <div class="form-row pt-4">
                  <div class="form-group col-md-12">
                    <label class="batch">Instructions</label>
                    <textarea v-model="applicants.instruction" class="text"></textarea>
                  </div>
                </div>
                <div class="btn1">
                  <button
                    type="submit"
                    class="btn btn-primary"
                    style="background-color: #2B3C4E; color:"
                  >
                    <loading v-if="isLoading" />
                    <span v-else>Submit</span>
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
// var myWidget = cloudinary.createUploadWidget(
// {
// cloudName: "dvcljsfid",
// uploadPreset: "me5otwzw"
// },
// (error, result) => {
// if (!error && result && result.event === "success") {
// console.log("Done! Here is the image info: ", result.info);
// console.log("Image Url " + result.info.url);
// } else {
// console.log(error);
// }
// }
// );
import AdminSidebar from "@/components/AdminSidebar.vue";
import Loading from "@/components/Loading.vue";
export default {
  name: "home",
  components: {
    AdminSidebar,
    Loading
  },
  data() {
    return {
      isLoading: false,
      apiResponse: {},
      applicants: {
        link: "",
        application_date: "",
        batch_id: "",
        instruction: "",
        // message: "",
        // error: "",
        image: ""
      },
      myWidget: "",
      message: "",
      error: "",

      error: []
    };
  },

  mounted() {
    this.myWidget = cloudinary.createUploadWidget(
      {
        cloudName: "dvcljsfid",
        uploadPreset: "me5otwzw"
      },
      (error, result) => {
        if (!error && result && result.event === "success") {
          console.log("Done! Here is the image info: ", result.info);
          console.log("Image Url " + result.info.url);
          this.applicants.image = result.info.url;
          console.log(this.image);
        } else {
          console.log(error);
        }
      }
    );
  },
  methods: {
    clicked() {
      this.myWidget.open();
    },

    // onFileChange(e) {
    // this.image = this.$refs.file.files[0];
    // var files = e.target.files || e.dataTransfer.files;
    // if (!files.length) return;
    // this.createImage(files[0]);
    // },

    // createImage(file) {
    // var image = new Image();
    // var reader = new FileReader();
    // var vm = this;
    // reader.onload = e => {
    // vm.image = e.target.result;
    // };
    // reader.readAsDataURL(file);
    // },
    removeImage: function removeImage(e) {
      this.applicants.image = "";
    },

    sendFile() {
      this.isLoading = true;

      this.$http
        .post("http://localhost:3000/attach/upload", this.applicants)
        .then(response => {
          // this.formData = "";
          this.applicants = "";

          alert("Application Created Successfully");
          console.log(response);
          this.$router.push("/preview");
          this.applicants = response.data;
        })
        .catch(error => {
          console.log(error);
        })
        .finally(() => {
          this.isLoading = false;
        });
    }
  }
};
</script>

<style scoped>
.wrap {
  height: 180vh;
}
.fileimg {
  height: 140px;
  width: 400px;
}
.sidebar {
  height: 180vh;
}

.otherSide {
  height: 180vh;
}

.inside {
  height: 180vh;
  width: 292px;
  box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.25);
  background-color: #ffffff;
}

.uploadfil {
  opacity: 0;
  position: absolute;
  cursor: pointer;
}

.john {
  width: 292px;
  height: 255px;
  background: #5abefd;
}

.image1 {
  padding-top: 75px;
  padding-left: 97px;
  padding-right: 115px;
  padding-bottom: 3px;
}

.name {
  font-family: Lato;
  font-style: normal;
  font-weight: bold;
  font-size: 15px;
  line-height: 24px;
  letter-spacing: -0.02em;
  color: #2b3c4e;
  padding-left: 97px;
  padding-top: 4px;
}

.mail {
  font-family: Lato;
  font-style: italic;
  font-weight: normal;
  font-size: 16px;
  line-height: 19px;
  letter-spacing: -0.02em;
  color: #2b3c4e;
  text-align: center;
}

.tool {
  height: 80vh;
  font-family: Lato;
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 19px;
  color: #2b3c4e;
}

.image2 {
  padding-top: 83px;
  padding-left: 43px;
}

.image3 {
  padding-top: 28px;
  padding-left: 43px;
}

.image4 {
  padding-top: 69px;
  padding-left: 43px;
}

.image33 {
  margin-top: 20px;
  padding-top: 10px;
  padding-left: 38px;
  border-left: 4px solid #31d283;
}

.first {
  padding-top: 137px;
  padding-left: 40px;
  opacity: 0.9;
  font-family: Lato;
  font-style: normal;
  font-weight: 100;
  font-size: 43.5555px;
  line-height: 52px;
  letter-spacing: -0.02em;
  color: #2b3c4e;
}

.apply {
  width: 95%;
  margin-left: 40px;
  padding-top: 62px;
}

.first_box {
  height: 108px;
  text-align: center;
}

#dotted {
  border: 0;
  border: 1.5px dashed #2b3c4e;
  border-radius: 6.2069px;
}

.files {
  border: 1.55172px dashed #2b3c4e;
  box-sizing: border-box;
  border-radius: 6.2069px;
  height: 108px;
}

.input_icons i {
  position: absolute;
  padding-top: 44px;
  padding-left: 154px;
}

.icon {
  padding: 10px;
  min-width: 50px;
  text-align: center;
}

.second_box {
  border: 1.5px solid #2b3c4e;
}

.second_box2 {
  border: 1.5px solid #2b3c4e;
  position: fixed;
  position: -webkit-sticky;
  position: sticky !important;
  top: 0;
}

.text {
  height: 120px;
  width: 100%;
  border: 1.5px solid #2b3c4e;
}

.batch {
  font-family: Lato;
  font-style: normal;
  font-weight: 550;
  font-size: 17px;
  line-height: 17px;
  color: #2b3c4e;
}

.btn {
  width: 50%;
  height: 50px;
  margin: auto;
  display: block;
  background-color: #2b3c4e;
  font-family: Lato;
  font-style: normal;
  font-weight: bold;
  font-size: 16px;
  line-height: 19px;
  color: #ffffff;
}

.btn3 {
  width: 30%;
  height: 40px;
  background-color: #2b3c4e;
  font-family: Lato;
  font-style: normal;
  font-weight: bold;
  font-size: 14px;
  line-height: 19px;
  color: #ffffff;
}

.btn1 {
  padding-top: 44px;
}

.btn:hover {
  color: #ffffff;
}
.visible {
  margin-top: -67px;
  margin-right: 6px;
  float: right;
  margin-right: 200px;
}
</style>