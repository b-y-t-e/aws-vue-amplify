<template>
    <div>
        <div class="col-md-6 mx-auto">
            <div class="card rounded-0">
                <div class="card-header">
                    <h3 class="mb-0">Main view</h3>
                </div>
                <div class="card-body">
                    <div class="form-group">
                        {{ message }}
                    </div>
                    <button class="btn btn-success btn-lg float-right"
                            @click="SignOut">
                        Logout
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { Auth, Logger, JS } from "aws-amplify";
export default {
  data() {
    return {
      message: "Connecting.."
    };
  },
  mounted() {
    var req = new XMLHttpRequest();
    req.open(
      "GET",
      "https://qmjoqchffd.execute-api.eu-west-1.amazonaws.com/dev/mp3-cognito?text=ala%20ma%20kota"
    );
    if (this.$store.state.session !== null)
      req.setRequestHeader(
        "Authorization",
        this.$store.state.session.idToken.getJwtToken()
      );
    req.onerror = s => {
      console.log(s);
      this.message = "CORS test error..";
    };
    req.onreadystatechange = s => {
      console.log(s);
      if (!(s.target.readyState == 4 && s.target.status == 200)) return;
      this.message = "CORS test success!!";
    };
    req.send(null);
  },
  methods: {
    SignOut: function(event) {
      Auth.signOut()
        .then(() => {
          console.log("sign out success");
          this.$store.state.session = null;
          this.$store.state.user = null;
          this.$router.push("/");
        })
        .catch(err => {
          console.log(err);
          alert(err);
        });
    }
  }
};
</script>
