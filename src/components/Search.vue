<template>
  <div class="search">
      <input type="text" placeholder="Find a place">
      <button>
        <img class="src-image" src="../assets/search.png"/>
      </button>
  </div>
</template>

<script>
export default {

}
</script>

<style>
    .search {
        position: absolute;
        top: 1px;
        left: 1%;
        z-index: 1000;
        display: flex;
    }
    .search input {
        padding: 5px 20px 5px 7px;
        border-radius: 5px;
        width: 300px;
    }
    .search button {
        cursor: pointer;
        margin-left: -20px;
        border-radius: 40%;
    }
    .src-image {
        width: 20px;
    }
</style>