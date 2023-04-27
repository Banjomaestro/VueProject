<template>
  <nav class="navbar space-navbar">

        <a class="navbar-item" href="#">
        <span class="navbar-item-text">SpaceVue</span>
        </a>
        <a class="navbar-item" href="#image-of-the-day">Image of the day</a>
        <a class="navbar-item" href="#asteroids">Asteroids</a>
        <a class="navbar-item" href="#cme">Coronal Mass Ejection</a>
        <a class="navbar-item" href="#marsPics">Martian pictures</a>
      
  </nav>
</template>
  
  <script>
  export default {
    name: 'SpaceNavBar',
  }
  </script>
  
  <style>
.space-navbar {
  position: fixed;
	top: 0;
	left: 0;
	width: 100%;
  background-color: #04172a;
  color: #fff;
  font-size: 1.2rem;
  font-weight: bold;
  z-index: 10 ;
  height : 5%;

}


.space-navbar .navbar-item-text {
  margin-left: 50px;
  margin-right: 50px;
  margin-top:10px
}

.space-navbar a.navbar-item {
  color: #fff;
  margin-left: 50px;
}

.space-navbar a.navbar-item:hover {
  background-color: #2e8b57;
  color: #fff;
}

.space-navbar .button.is-primary {
  background-color: #2e8b57;
}

.space-navbar .button.is-primary:hover {
  background-color: #228b22;
}

.space-navbar .navbar-brand img {
  height: 10px;
  margin-right: 5px;
}
</style>
