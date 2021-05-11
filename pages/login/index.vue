<template>
  <div class="container-fluid">
    <div class="row justify-content-center">
      <div class="col-xl-10 col-lg-12 col-md-9">
        <div class="card o-hidden border-0 shadow-lg my-5">
          <div class="card-body p-0">
            <div class="row">
              <div class="col-lg-6 d-none d-lg-block bg-login-image"></div>
              <div class="col-lg-6">
                <div class="p-5">
                  <div class="text-center">
                    <h1 class="h4 text-gray-900 mb-4">Welcome Back!</h1>
                  </div>
                  <form class="user">
                    <div class="form-group">
                      <input
                        id="exampleInputEmail"
                        v-model="auth.Username"
                        type="text"
                        class="form-control form-control-user"
                        aria-describedby="emailHelp"
                        placeholder="Enter Email Address..."
                      />
                    </div>
                    <div class="form-group">
                      <input
                        id="exampleInputPassword"
                        v-model="auth.Password"
                        type="password"
                        class="form-control form-control-user"
                        placeholder="Password"
                      />
                    </div>
                    <div class="form-group">
                      <div class="custom-control custom-checkbox small">
                        <input
                          id="customCheck"
                          type="checkbox"
                          class="custom-control-input"
                        />
                        <label class="custom-control-label" for="customCheck"
                          >Remember Me</label
                        >
                      </div>
                    </div>
                    <a
                      href="javascript:void(0)"
                      class="btn btn-primary btn-user btn-block"
                      @click="submit"
                    >
                      Login
                    </a>
                    <hr />
                  </form>
                  <hr />
                  <div class="text-center">
                    <a class="small" href="#">Forgot Password?</a>
                  </div>
                  <div class="text-center">
                    <a class="small" href="#">Create an Account!</a>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { mapMutations } from 'vuex'
export default {
  auth: false,
  data() {
    return {
      auth: {
        Username: null,
        Password: null,
      },
    }
  },
  mounted() {
    if (this.$auth.loggedIn) {
      this.$router.push('/')
    }
  },
  methods: {
    ...mapMutations(['SET_IS_AUTH']),
    submit() {
      this.$auth
        .loginWith('local', {
          data: {
            Username: this.auth.Username,
            Password: this.auth.Password,
          },
        })
        .then((response) => {
          this.SET_IS_AUTH(true)
          this.$router.push('/')
        })
    },
  },
}
</script>
