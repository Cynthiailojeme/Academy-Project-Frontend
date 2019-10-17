<template>
    <div>
        <div class="top">
            <div class="left">
                <h1>Take Assessment</h1>
                <p class="limited">Click the button below to start assessment, you have limited time for this test</p>
            </div>
            <!-- <div class="right">
                <h2>Timer</h2>
            </div> -->
        </div>

        <div class="hourglass">
            <center>
                <img src="../assets/hourglass.svg" alt="timer" class="time">
                <p v-if="days!=0">We have {{days}} days left until the next assessment
                <br>Watch this space</p>
                <p v-if="showing===true">Date of Assessment Passed</p>
                <div class="dropdown">
                    <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                        Take Assessment
                    </button>
                    <div class="dropdown-menu" aria-labelledby="dropdownMenuButton" v-if="days===0">
                        <a class="dropdown-item" @click="itemClicked(questionset)" v-for="(questionset, index) in questionsets" :key="index">
                                {{ questionset.nameOfSet }}
                        </a>
                    </div>

                    <!-- Modal -->
                    <div class="modal fade" id="exampleModalCenter" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
                        <div class="modal-dialog modal-dialog-centered" role="document">
                            <div class="modal-content">
                                <div class="modal-header">
                                    <h5 class="modal-title" style="margin-left: 100px;" id="exampleModalLongTitle">Assessment Instructions</h5>
                                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                                            <span aria-hidden="true">&times;</span>
                                    </button>
                                </div>
                                <div class="modal-body"><p>This assessment contains {{ number }} questions for {{ name }}.</p>
                                    <p>You have {{ duration }} mins to complete this assessment.</p>
                                    <p>Click on the start button to begin</p>
                                    <p>Goodluck!</p>
                                    <p>
                                        <router-link :to="{name:'Questions', params:{id}}">
                                            <button class="modalbtn" type="button" data-dismiss="modal">START</button>
                                        </router-link>
                                    </p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </center>
        </div>
    </div>
</template>

<script>
import moment from 'moment';



export default {
  name: 'TakeAssessment',
  data() {
      return {
        questionsets: [],
        questionset: {},
        dateOfAssess: null,
        index: null,
        days: 0,
        showing: false,
        name: "",
        duration: "",
        number: "",
        id: ""
       }
     },
    components: {},
    mounted() {
        const url = "http://localhost:3000/api/questionset/all"
        this.$http.get(url)
        .then(response => {
        console.log(response.body)
        this.questionsets = response.body
        console.log(response.body[response.body.length -1])
        this.dateOfAsess = response.body[response.body.length -1].dateOfAsess
        var now = moment(new Date()); //todays date
        var end = moment(this.dateOfAsess); // another date
        var duration = moment.duration(end.diff(now));
        var show = now.isAfter(end);
    
        if(this.show){
            console.log("date passed")
            this.showing = true
        }
        else{
            console.log("date not passed")
             this.days = duration.days();
             console.log(this.days)
        console.log(this.dateOfAsess)
        }
        
    });
    },
computed: {},
 methods: {
        itemClicked: function(questionset) {
            this.name = questionset.nameOfSet;
            this.duration = questionset.duration;
            this.number = questionset.quiz.length;
            this.id = questionset._id;
            console.log(questionset._id)
			$("#exampleModalCenter").modal('show');
        }
    }
}
</script>

<style scoped>
.top {
    display: flex;
    justify-content: space-between;
}
.left {
    float: right;
}
.right {
    float: right;
}
.limited{
    width: 510px;
    font-family: Lato;
    font-style: italic;
    font-weight: bold;
    font-size: 15px;
    color: #2B3C4E;
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
.top > p {
    font-family: Lato;
    font-style: italic;
    font-weight: 500;
    font-size: 16px;
    color: #2B3C4E;
}
h2 {
    font-family: Lato;
    font-style: normal;
    font-weight: normal;
    font-size: 14px;
    text-align: left;
    margin-right: 100px;
    line-height: 52px;
    color: #4F4F4F;
}
.hourglass {
    width: 100%;
    margin-top: 100px;
}
.time {
    padding-bottom: 20px;
}
.hourglass > p {
    font-family: Lato;
    font-style: normal;
    font-weight: normal;
    font-size: 16.7273px;
    text-align: center;
    color: #4F4F4F;
}
.dropdown-toggle {
    width: 50%;
    max-width: 205px;
    height: 41px;
    background: #B1B1B1;
    border-radius: 4px;
    border: none;
    font-family: 'Lato', sans-serif;
    font-style: normal;
    font-weight: bold;
    font-size: 16px;
    color: #FFFFFF;
    margin-left: auto;
    margin-right: auto;
    display: block;
}
.dropdown-menu {
    width: 205px;
}
a {
    color: #2B3C4E;
    text-decoration: none;
}
a:first-letter {
    text-transform:capitalize;
    color: #2B3C4E;
}
.modalbtn {
    width: 150px;
    height: 50px;
    background: #2B3C4E;
    border-radius: 4px;
    border: none;
    font-family: 'Lato', sans-serif;
    font-style: normal;
    font-weight: bold;
    font-size: 16px;
    color: #FFFFFF;
    margin-left: auto !important;
    margin-right: auto !important;
    text-align: center !important;
    display: block;
}
.modal-title {
    text-align: center !important;
}
</style>