<template>
  <div class="wrap">
    <div class="whole-body">
      <div>
        <img src="../assets/enyata-logo.png" class="img" />
      </div>

      <div class="section">
        <div>
          <h1>Enyata software Engineering limited is recieving applications into her academy.</h1>
          <div class="text">
            <h3>{{applicants.instruction}}</h3>
          </div>
        </div>

        <div class="prior">No prior knowledge of coding is required.</div>
        <div class="requirement">
          <h6>Requirement</h6>
          <ul>
            <li>
              <b>Intelligent, young & Smart</b>
            </li>
            <li>
              <b>Graduates from polytechnics</b>
            </li>
            <li>
              <b>Graduate from Universities and other related institutions</b>
            </li>
            <li>
              <b>Any discipline of study</b>
            </li>
            <li>
              <b>Any gender</b>
            </li>
          </ul>
          <p>
            <b>Application closes {{applicants.application_date|longDate }}</b>
          </p>
        </div>
      </div>
    </div>

    <div class="foot">
      <p>Kindly follow the link below to apply</p>
      <span class="link">
        <router-link :to="{name: 'application-form'}" style="color:ffff;">{{applicants.link}}</router-link>
      </span>
    </div>
    <social-sharing
      url="https://enyata.com"
      title="Enyata Academy Recruitment"
      description="Enyata academy is putting out opportunities to young aspiring developers to learn and grow in the software engineering world."
      inline-template
      class="networks"
    >
      <div>
        <button style="background: #5abefd;">
          <network network="facebook">
            <i class="fa fa-fw fa-facebook"></i> Facebook
          </network>
        </button>
        <button style="background: #5abefd;">
          <network network="googleplus">
            <i class="fa fa-fw fa-google-plus"></i> Google +
          </network>
        </button>
        <button style="background: #5abefd;">
          <network network="linkedin">
            <i class="fa fa-fw fa-linkedin"></i> LinkedIn
          </network>
        </button>
        <button style="background: #5abefd;">
          <network network="pinterest">
            <i class="fa fa-fw fa-pinterest"></i> Pinterest
          </network>
        </button>
        <button style="background: #5abefd;">
          <network network="reddit">
            <i class="fa fa-fw fa-reddit"></i> Reddit
          </network>
        </button>
        <button style="background: #5abefd;">
          <network network="twitter">
            <i class="fa fa-fw fa-twitter"></i> Twitter
          </network>
        </button>
        <button style="background: #5abefd;">
          <network network="vk">
            <i class="fa fa-vk"></i> VKontakte
          </network>
        </button>
        <button style="background: #5abefd;">
          <network network="weibo">
            <i class="fa fa-weibo"></i> Weibo
          </network>
        </button>
        <button style="background: #5abefd;">
          <network network="whatsapp">
            <i class="fa fa-fw fa-whatsapp"></i> Whatsapp
          </network>
        </button>
      </div>
    </social-sharing>
  </div>
</template>


<script>
export default {
  name: "home",
  data() {
    return {
      apiResponse: {},
      applicants: [],

      error: {}
    };
  },

  components: {},

  mounted() {
    this.$http.get("http://localhost:3000/attach").then(response => {
      // console.log(response.data)
      // console.log (response.data[response.data.length -1])
      this.applicants = response.data[response.data.length - 1];
    });
  },

  filters: {
    longDate: function(val) {
      var now = new Date(val);
      var months = [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May",
        "Jun",
        "Jul",
        "Aug",
        "Sep",
        "Oct",
        "Nov",
        "Dec"
      ];
      return (
        now.getDate() +
        "th " +
        "" +
        months[now.getMonth()] +
        "," +
        " " +
        now.getFullYear()
      );
    }
  }
};
</script>


<style scoped>
.wrap {
  background: url("../assets/banner.png");
  background-repeat: no-repeat;
  background-position: right;
  background-size: contain;
  height: 130vh;
}
.whole-body {
  margin-left: 30px;
}

.text {
  width: 50%;
}
.section {
  margin-top: 50px;
}
.section h1 {
  font-size: 25px;
}
.section h3 {
  color: #2b3c4e;
  font-size: 18px;
}
.img {
  width: 120px;
  height: 130px;
}
h1 {
  font-family: "Lato", san-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 20px;
}
h3 {
  font-family: "Lato", san-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
}
.prior {
  background-color: #2b3c4e;
  width: 100%;
  max-width: 400px;
  height: 30px;
  color: #fff;
  text-align: center;
  font-family: "Lato", san-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 18px;
  margin-top: 50px;
}

.requirement {
  margin-top: 50px;
}

.requirement h6 {
  font-family: "Lato", san-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 18px;
}

.requirement p {
  margin-top: 30px;
  font-family: "Lato", san-serif;
  font-style: normal;
  font-weight: bold;
}

.foot {
  background-color: #2b3c4e;
  color: #fff;
  text-align: center;
  width: 100%;
  margin-top: 150px;
  padding: none;
}
.btn {
  width: 10%;
  height: 50px;
  margin: auto;
  display: block;
  background-color: #92979d;
  font-family: Lato;
  font-style: normal;
  font-weight: bold;
  font-size: 16px;
  line-height: 19px;
  color: #ffffff;
}
a {
  color: #fff;
  text-decoration: none;
}
.networks {
  margin-left: 15%;
  margin-top: 5px;
}
</style>