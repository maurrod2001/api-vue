<template>
  <div class="hello ">
    <h1 class="pt-3 text-success">{{ msg }}</h1>
    <div class="text-center container">
      <main class="form-signin">
        <form>
          <h1 class="h3 mb-3 fw-normal">Please sign in</h1>

          <div class="form-floating">
            <input type="email" class="form-control text-danger" id="floatingInput" placeholder="name@example.com">
            <label class="text-dark" for="floatingInput">email</label>
          </div>
          <div class="form-floating">
            <input type="password" class="form-control" id="floatingPassword" placeholder="Password"
              autocomplete="email">
            <label class="text-dark" for="floatingPassword">Password</label>
          </div>

        </form>
        <button class="w-100 btn btn-lg btn-success " type="submit" @click="getLogin()">Sign in</button>
        <p class="mt-5 mb-3 text-muted">&copy; 2020-2021</p>
        <button class="btn btn-outline-danger" @click="test()">test</button>

      </main>
    </div>

  </div>
  <br>
</template>

<script>
import router from '@/router';
import axios from 'axios'
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods: {
    getLogin() {
      axios.get('http://localhost:3000/getLogin')
        .then(function (response) {
          console.log(response);
          console.log(response.data[length].username);
          var test = response.data.length
          console.log(test)
          for (var i = 0; i < test; i++) {
            alert(response.data[i].username)
          }

        })
        .catch(function (error) {
          console.log(error);
        });
      router.push("about")
    },
    test() {
      router.push("medic")
    }
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.form-signin {
  width: 100%;
  max-width: 330px;
  padding: 15px;
  margin: auto;
}


.form-signin .form-floating:focus-within {
  z-index: 2;
}

.form-signin input[type="email"] {
  margin-bottom: -1px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}

.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
</style>
