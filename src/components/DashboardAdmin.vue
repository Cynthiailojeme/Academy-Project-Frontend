<template>
  <div>
    <h1>Dashboard</h1>
    <div class="total-status">
      <div class="date">
        <p>Current Applications</p>
        <span>{{applicants.total}}</span>
        <div class="for-status">current application</div>
        <p class="small-text"></p>
      </div>
      <div class="status">
        <p>Total Application</p>
        <span>{{applicants.total}}</span>
        <div class="for-status2"></div>
        <p class="small-text">All entries so far</p>
      </div>
    </div>
    <div class="update-assessment d-flex">
      <div class="update">
        <h4>History</h4>
        <p>Update</p>
        <div class="table-box">
          <table class="table table-borderless">
            <tbody>
              <tr>
                <router-link :to="{name: 'entries'}" class="new">
                  <td scope="row">Applicants</td>
                  <td>{{applicants.total}} students</td>
                  <td></td>
                </router-link>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      <div class="take-assessment ml-4">
        <h4 class="create-assessment">Compose Assessment</h4>
        <div class="take-assessment-body">
          <p>Compose test question for an incoming academy students</p>
          <router-link :to="{name: 'Admin-compose'}" class="links">
            <button>Compose Assessment</button>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "home",
  components: {},
  data() {
    return {
      applicants: []
      // attach:[]
    };
  },
  mounted() {
    this.$http.get("http://localhost:3000/recruit/total").then(response => {
      console.log(response);
      this.applicants = response.data;
    });
  }
};
</script>


<style scoped>
h1 {
  font-family: Lato;
  font-style: normal;
  font-weight: 300;
  font-size: 43.5555px;
  letter-spacing: -0.02em;
  color: #2b3c4e;
}
.head {
  font-family: "Lato", sans-serif;
  font-style: normal;
  font-weight: 300;
  font-size: 43.5555px;
  letter-spacing: -0.02em;
  color: #2b3c4e;
}

.head span {
  font-family: "Lato", sans-serif;
  font-style: italic;
  font-weight: 500;
  font-size: 16px;
  color: #2b3c4e;
}

.total-status {
  display: flex;
  margin-top: 60px;
}

.date {
  font-family: "Lato", sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 14px;
  color: #4f4f4f;
}

.date span {
  font-family: "Nunito Sans", sans-serif;
  font-style: normal;
  font-weight: 300;
  font-size: 48px;
  line-height: 65px;
  text-align: center;
  color: #2b3c4e;
}

.small-text {
  font-family: "Lato", sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
  color: #4f4f4f;
}

.new {
  color: #000 !important;
  font-size: 18px;
  font-weight: bold;
  display: block;
}
.new:hover {
  text-decoration: none;
}

.status {
  margin-left: 150px;
}
.status {
  font-family: "Nunito Sans", sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 14px;
  text-align: center;
  color: #4f4f4f;
}

.status span {
  font-family: "Nunito Sans", sans-serif;
  font-style: normal;
  font-weight: 300;
  font-size: 48px;
  text-align: center;
  color: #2b3c4e;
}
.for-status {
  width: 148px;
  height: 4px;
  background: #006df0;
  border-radius: 4px;
}
.for-status2 {
  height: 4px;
  width: 148px;
  height: 4px;
  background: #00f026;
  border-radius: 4px;
}
.for-status3 {
  width: 148px;
  height: 4px;
  background: #f09000;
  border-radius: 4px;
}
.create-assessment {
  font-family: Lato;
  font-style: normal;
  font-weight: bold;
  font-size: 16px;
  line-height: 19px;
  letter-spacing: -0.02em;
  color: #2b3c4e;
  padding-left: 31px;
  padding-top: 26px;
}
h4 {
  font-family: Lato;
  font-style: normal;
  font-weight: bold;
  font-size: 16px;
  line-height: 19px;
  letter-spacing: -0.02em;
  color: #2b3c4e;
}
p {
  font-family: Nunito Sans;
  font-style: normal;
  font-weight: normal;
  color: #4f4f4f;
}
.update-assessment {
  margin-top: 77px;
}
.update {
  font-family: "Lato", sans-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 16px;
  letter-spacing: -0.02em;
  color: #2b3c4e;
  margin-top: 53px;
  width: 482px;
  height: 453px;
}

.take-assessment {
  width: 482px;
  height: 453px;
  border: 1px solid #ececf9;
  box-sizing: border-box;
  border-radius: 4px;
}

.take-assessment {
  font-family: "Lato", sans-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 16px;
  letter-spacing: -0.02em;
  color: #2b3c4e;
  margin-left: 34px;
  margin-top: 25px;
}

.take-assessment-body {
  margin-top: 189px;
}

.take-assessment-body {
  font-family: "Lato", sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 16.7273px;
  text-align: center;
  color: #4f4f4f;
}
button {
  width: 50%;
  max-width: 205px;
  height: 41px;
  background: #b1b1b1;
  border-radius: 4px;
  font-family: "Lato", sans-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 16px;
  color: #ffffff;
  margin-left: auto;
  margin-right: auto;
  display: block;
  border: none;
}
.links {
  color: #ffffff;
}
.create-assessment {
  font-family: Lato;
  font-style: normal;
  font-weight: bold;
  font-size: 16px;
  line-height: 19px;
  letter-spacing: -0.02em;
  color: #2b3c4e;
  padding-left: 31px;
}
tbody tr {
  font-family: Nunito Sans;
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 22px;
  text-align: center;
  color: #4f4f4f;
  width: 100%;
  height: 66px;
}
tbody > tr:hover {
  width: 100%;
  height: 66px;
  background: #ffffff;
  box-shadow: 8px 18px 20px rgba(79, 79, 79, 0.3);
  border-left: 7px solid #5abefd;
  border-radius: 8px;
}
</style>