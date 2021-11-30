<template>
  <div class="contact-div">
    <h3>GET IN TOUCH</h3>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
    <div class="card">
      <div class="card-header">
        <h5>Contact Form</h5>
      </div>
      <div class="card-body">
        <div class="row ">
          <div class="col-md-6">
            <label for="name" class="form-label">Name *</label>
            <input type="text" id="name" class="form-control rounded-0 border-0">  
          </div>
          <div class="col-md-6 ">
            <label for="email" class="form-label">Email Address *</label>
            <input type="email" id="email" class="form-control rounded-0 border-0">
          </div>
        </div>
        <div class="row mt-2">
          <div class="col-md-12">
            <label for="message" class="form-label">Message *</label>
            <textarea class="form-control rounded-0 border-0" id="message"></textarea>
          </div>
        </div>
        <div class="float-end mt-2">
          <button type="button" class="rounded-0 p-2 px-4 border-0 text-white">Send</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .contact-div{
    margin-left: 30%;
    margin-right: 30%;
  }
  @media screen and (max-width: 1200px){
    .contact-div{
      margin-left: 20%;
      margin-right: 20%;
    }
  }
  @media screen and (max-width: 500px){
    .contact-div{
      margin-left: 0%;
      margin-right: 0%;
    }
  }
</style>