<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container-fluid">
      <a class="navbar-brand" href="/">Store</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link" aria-current="page" href="/products">All Products</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/products/new">New Product</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/signup">Sign up</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/login">Log in</a>
          </li>
          <li class="nav-item">
            <a class="nav-link disabled">Log out</a>
          </li>
        </ul>
        <form class="d-flex">
          <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search" />
          <button class="btn btn-outline-success" type="submit">Search</button>
        </form>
      </div>
    </div>
  </nav>
  <!-- Older nav bar -->
  <!-- <nav>
    <router-link to="/">Home</router-link>
    |
    <router-link to="/products">All Products</router-link>
    |
    <router-link to="/products/new">New Product</router-link>
    |
    <router-link to="/signup">Sign up</router-link>
    |
    <router-link to="/login">Log in</router-link>
    |
    <router-link to="/logout">Log out</router-link>
  </nav> -->
  <router-view />
</template>

<style>
#app {
  font-family: Century Gothic, CenturyGothic, AppleGothic, sans-serif;
  background-image: url("./assets/swirl_pattern.webp");
}
</style>
