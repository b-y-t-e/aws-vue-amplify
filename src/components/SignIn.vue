<template>
    <div>
        <div class="col-md-6 mx-auto">
            <div class="card rounded-0">
                <div class="card-header">
                    <h3 class="mb-0">Login</h3>
                </div>
                <div class="card-body">
                    <div class="form-group">
                        <label>Username</label>
                        <input type="text" v-model="email" class="form-control form-control-lg rounded-0" required="">
                    </div>
                    <div class="form-group">
                        <label>Password</label>
                        <input type="password" v-model="password" class="form-control form-control-lg rounded-0" required=""
                               autocomplete="new-password">
                    </div>
                    <button class="btn btn-success btn-lg float-right"
                            @click="signin">
                        Login
                    </button>
                    <button class="btn btn-primary btn-lg float-right" style="margin-right: 10px;"
                            @click="signup">
                        Register
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
      email: "",
      password: ""
    };
  },
  methods: {
    signin() {
      Auth.signIn(this.email, this.password)
        .then(user => {
          console.log("sign in success", user);
          Auth.currentSession()
            .then(session => {
              /*console.log(session);
              console.log(session.accessToken);
              console.log(session.idToken);
              console.log(session.refreshToken);*/
              this.$store.state.session = session;
              this.$store.state.user = user;
              this.$router.push("/main");
              return user;
            })
            .catch(err => { console.log(err); alert(err); });
        })
        .catch(err => {
          console.log(err);
          alert(err && err.message ? err.message : err);
        });
    },
    signup(){
      this.$router.push("/signup");
    }
  }
};
</script>
