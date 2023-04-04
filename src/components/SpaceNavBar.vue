<template>
  <nav class="navbar space-navbar">

    <div class="navbar-menu">
      <div class="navbar-start">
        <a class="navbar-item" href="#">
        <img src="/src/assets/logo.png" alt="Space Logo" />
        <span class="navbar-item-text">SpaceVue</span>
        </a>
        <a class="navbar-item" href="#">Home</a>
        <a class="navbar-item" href="#">News</a>
        <a class="navbar-item" href="#">Missions</a>
        <a class="navbar-item" href="#">Gallery</a>
        <a class="navbar-item" href="#">About</a>
      </div>
    </div>
  </nav>
</template>
  
  <script>
  export default {
    name: 'SpaceNavBar',
  }
  </script>
  
  <style>
.space-navbar {
  background-color: #04172a;
  color: #fff;
  font-size: 1.2rem;
  font-weight: bold;
}

.space-navbar .navbar-item-text {
  margin-left: 50px;
  margin-right: 50px;
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
  height: 50px;
  margin-right: 5px;
}
</style>
