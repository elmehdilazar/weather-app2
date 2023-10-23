<template>
<div class="app">
  <div class="header container h-100 p-5">
    <h1 class="mb-5">Weather App</h1>
    <div class="d-flex justify-content-center h-100">

<div class="searcbar w-50 mx-2">
  <input type="text" class="input form-control" placeholder="Enter a City">
</div>
<button type="button" class="btn-search btn btn-primary">Search <i class="fa fa-search" aria-hidden="true"></i></button>

    </div>
  </div>
</div>
</template>

<style lang="scss">
body{
  background-color: #121212 !important;

}
.header{
  background-color: #212730;
  border-radius: 20px;
  margin-top: 5rem;
  color: #fff;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  text-align: center;
}
.btn-search{
  background-image: linear-gradient(to right,cyan,magenta);
}
</style>
