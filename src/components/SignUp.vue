<template>
    <div>
        <div class="col-md-6 mx-auto">
            <div class="card rounded-0">
                <div class="card-header">
                    <h3 class="mb-0">Register</h3>
                </div>
                <div class="card-body">
                    <div class="form-group">
                        <label>Username</label>
                        <input type="text" v-model="login" class="form-control form-control-lg rounded-0" required="">
                    </div>
                    <div class="form-group">
                        <label>Email</label>
                        <input type="email" v-model="email" class="form-control form-control-lg rounded-0" required="">
                    </div>
                    <div class="form-group">
                        <label>Password</label>
                        <input type="password" v-model="password" class="form-control form-control-lg rounded-0" required=""
                               autocomplete="new-password">
                    </div>
                    <button class="btn btn-success btn-lg float-right"
                            @click="signUp">
                        Register
                    </button>
                    <button class="btn btn-info btn-lg float-right" style="margin-right: 10px;"
                            @click="back">
                        Back
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
      login: "",
      email: "",
      password: ""
    };
  },
  methods: {
    signUp: function(event) {
      Auth.signUp(this.login, this.password, this.email)
        .then(data => {
          console.log("sign up success", data);
          alert('Please check your email');
          this.$router.push("/");
        })
        .catch(err => {
          console.log(err);
          alert(err && err.message ? err.message : err);
        });
    },
    back() {
      this.$router.push("/");
    }
  }
};
</script>
