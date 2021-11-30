<template>
  <div>
    <div class="container">
      <div class="py-5 row">
        <div class=" col-md-4 col-lg-3 col-xl-3 col-xxl-2">
          <router-link class="router-link" to="/">VIDEO GAMES</router-link>
        </div>
        <div class="col-md-2">
          <router-link class="router-link " to="/contact">CONTACT</router-link>
        </div>
      </div>
    </div>
    <div class="container-fluid">
      <router-view/>
    </div>
  </div>
</template>

<style>

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  font-family: 'Mulish', sans-serif;
  background-image: linear-gradient(#081221, #03080f);
  background-repeat: no-repeat;
  background-attachment: fixed;
  margin: 0;
  height: 100%;
  color: #c1d1e8 !important;
}

a, h1, h2, h3, h4, h5, h6, label {
  font-family: 'Montserrat', sans-serif;
  color: #ffffff !important;
}

.router-link {
  text-decoration: none;
  display: block;
  font-size: 22px;
  font-weight: bold;
}

/*@media screen and (min-width:  810px){
  .router-link{
    display: inline-block;
  }
}*/

.router-link:hover {
  color: #cdcdcd !important;
}

.router-link:active {
  color: #898989 !important;
}

.card {
  background: #0e1a2b !important;
}

button {
  font-family: 'Montserrat', sans-serif;
  background: #5692e8 !important;
}

input, select, textarea {
  background: #182c47 !important;
  color: #c1d1e8 !important;
  border: none;
}

</style>
