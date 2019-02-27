<template>
  <div id="app">
    <div id="nav">

      <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <a class="navbar-brand" href="#"> Nerd Stuff</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav mr-auto">
            <li class="nav-item active">
              <a><router-link to="/">Home</router-link></a>
            </li>
            <li class="nav-item">
              <router-link to="/products/new">New Product</router-link>
            </li>
          </ul>
        </div>
      </nav>


    </div>
    <div class="container">
      <router-view/>
    </div>


  </div>
</template>




