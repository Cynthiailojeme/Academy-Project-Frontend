<template>
    <div class="dashboard">
        <div>
            <AdminSidebar/>
        </div>

        <div class="main">
            <h1>
                Edit Assessment
            </h1>

            <form>
            <div class="form-row">
                <div class="form-group col-md-12">
                    <label class="headings">Name of Assessment</label>
                    <input type="text" class="form-control correct" v-model="questionset.nameOfSet" required>
                </div>
            </div>

            <div class="form-row">
                <div class="form-group col-md-12">
                    <label class="headings">Duration for the assessment (minutes)</label><br>
                    <input type="number" class="form-control correct" v-model="questionset.duration" required>
                </div>
            </div>

           <div class="form-row">
                <div class="form-group col-md-12">
                    <label class="headings">Date of Assessment</label>
                    <input type="date" class="form-control correct" v-model="questionset.dateOfAsess" required>
                </div >
            </div>

            <br>
            <div class="form-row">
                <div class="form-group col-md-6">
                    <label class="headings">Questions</label>
                </div>
                    <!-- <div class="files"  v-if="!image">
                        <input type="file" class="uploadfil" ref="file" @change="onFileChange" required>
                        <p><img src="../assets/plus.svg" class="icon">Choose File</p>
                    </div>
                    <div v-else>
                        <img :src="image" class="fileimg"/>
                        <input type="file" name="image" style="display:none">
                        <button @click="removeImage">Remove image</button>
                    </div> -->
            </div>
            
            
            <div v-for="(quiz, index) in questionset.quiz" :key="index">  
            <div class="form-group">
                <label>Question {{ index+1 }}</label>
                <textarea class="form-control rounded-1" rows="3" v-model="quiz.question" required></textarea>
                <br>
                <img class="fileimg" v-if="quiz.img" :src="quiz.img" required>
            </div>

            <div class="form-row">
                <div class="form-group col-md-6">
                    <label>Option A</label>
                    <input type="text" class="form-control" v-model="quiz.options[0]">
                </div>
                <div class="form-group col-md-6">
                    <label>Option B</label>
                    <input type="text" class="form-control" v-model="quiz.options[1]">
                </div>
            </div>

            <div class="form-row">
                <div class="form-group col-md-6">
                    <label>Option C</label>
                    <input type="text" class="form-control" v-model="quiz.options[2]">
                </div>
                <div class="form-group col-md-6">
                    <label>Option D</label>
                    <input type="text" class="form-control" v-model="quiz.options[3]">
                </div>
            </div>

            <div class="form-row">
                <div class="form-group col-md-12">
                    <label>Answer</label>
                    <input type="text" class="form-control correct" v-model="quiz.correctAnswer" required>
                </div>
            </div>
            <br>
            </div>

            <br>

            <div class="form-row">
                <div class="form-group col-md-12">
                    <center>
                        <button type="submit" class="button" @click.prevent="editSet">SAVE</button>
                    </center>
                </div>
            </div>
        </form>

        </div>
    </div>
</template>

<script>
import AdminSidebar from '@/components/AdminSidebar.vue'

export default {
    name: 'home',
    props: ['id'],
    data() {
        return{
            questionset: {},
            quiz: {},
            question: "",
            takenassessment: false,
        };
    },
components: {
       AdminSidebar
  },
  mounted() {
    let id = this.$route.params.id;
    let headers = {
      "x-access-token": localStorage.getItem("token")
    };
    this.$http
      .get("http://localhost:3000/api/questionset/single/" + id, { headers })
      .then(response => {
        console.log(response.body);
        this.questionset = response.body;
      })
      .catch(err => {
        console.log(err);
      });
  },
  methods: {
    editSet() {
        console.log(this.questionset)
        let id = this.questionset._id
        this.$http.put('http://localhost:3000/api/questionset/update/'+id, this.questionset)
        .then(response =>{
            console.log(response)
            this.questionset = response.data
            this.$router.push("/Assessment-history")
            // this.questionsets.push(response.data);
        })
    }
},
}
</script>

<style scoped>
.dashboard {
    height: 100%;
}
.main {
    height: 100%;
    margin-left: 300px;
    padding: 80px 70px 50px 70px;
}
h1 {
    font-family: Lato;
    font-style: normal;
    font-weight: 300;
    font-size: 43.5555px;
    line-height: 52px;
    letter-spacing: -0.02em;
    color: #2B3C4E;
}
form{
    padding-top: 30px;
}
.files {
    border: 1.55172px dashed #2B3C4E;
    box-sizing: border-box;
    border-radius: 6.2069px;
    height: 108px;
    width: 90% !important;
}
.fileimg {
    height: 200px;
    width: 200px;
}
.block {
    display: flex;
    flex-direction: column;
    margin: 20px;
}
.text {
    color: #1abc9c;
    font-size: 20px;
    font-family: 'Roboto Condensed', serif;
    font-weight: 400;
    margin-top:10px;
    margin-bottom: 10px;
    text-align: center;
}
.digit {
    color: #ecf0f1;
    font-size: 20px;
    font-weight: 100;
    font-family: 'Roboto', serif;
    margin: 10px;
    text-align: center;
}
.form-group > .files > p {
    font-family: Avenir;
    font-size: 16px;
    text-align: center;
    padding: 50px 0;
    color: #2B3C4E;
  }
.uploadfil {
    opacity: 0;
    position: absolute;
    cursor: pointer;
}
.uploaded {
    width: 100%;
    height: 100%;
}
.icon{
    margin-right: 15px;
}
.form-group > label {
    font-family: Lato;
    font-style: normal;
    font-weight: normal;
    font-size: 14px;
    line-height: 17px;
    color: #2B3C4E;
}
.buttonholder {
    text-align: center;
    padding: 50px;
}
.buttonholder2 {
    text-align: center;
    padding: 20px;
}
button {
    margin-left: auto;
    margin-right: auto;
    width: 125px;
    height: 41px;
    background: #2B3C4E;
    border-radius: 4px;
    border: none;
    font-family: Lato;
    font-style: normal;
    font-weight: bold;
    font-size: 16px;
    line-height: 19px;
    color: #FFFFFF;
}
.button2 {
    background: #2B3C4E;
    border-radius: 4px;
    width: 205px;
    height: 41px;
}
textarea {
    border: 1.5px solid #2B3C4E;
    box-sizing: border-box;
    border-radius: 4px;
    width: 95%;
}
input {
    border: 1.5px solid #2B3C4E;
    height: 41px;
    box-sizing: border-box;
    border-radius: 4px;
    width: 90%;
}
.correct {
    border: 1.5px solid #2B3C4E;
    height: 41px;
    box-sizing: border-box;
    border-radius: 4px;
    width: 95%;
}
.h6{
    font-family: Lato;
    font-style: normal;
    font-weight: normal;
    font-size: 14px;
    line-height: 17px;
    text-align: center;
    color: #2B3C4E;
}
.headings {
    font-weight: 200 !important;
    font-size: 20px !important;
    color: #2B3C4E !important;
}
</style>