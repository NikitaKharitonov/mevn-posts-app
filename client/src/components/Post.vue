<template>
  <div class="post">
    <div class="top">
      <div class="date">{{ date.toUTCString() }}</div>
      <div class="dropdown">
        <button class="dropbtn">v</button>
        <div class="dropdown-content">
          <a href="">Delete</a>
          <a href="">Archive</a>
          <a href="">Edit</a>
        </div>
      </div>
    </div>


    <p class="postText">
      {{ text }}
    </p>
  </div>
</template>

<script>
export default {
  name: "Post",
  props: {
    text: String,
    date: Date,
  }
}
</script>

<style scoped>
.top{
  display: flex;
  justify-content: space-between;
}
.post {
  background: #333336;
  border-radius: 4px;
  padding: 10px;
  height: fit-content;
  margin-bottom: 8px;
}

.date {
  color: darkgrey;
}

/* Dropdown Button */
.dropbtn {
  background: inherit;
  color: white;
  border: none;
}

/* The container <div> - needed to position the dropdown content */
.dropdown {
  position: relative;
  display: inline-block;

}

/* Dropdown Content (Hidden by Default) */
.dropdown-content {
  display: none;
  position: absolute;
  background-color: #444446;
  font-size: 14px;
  width: 140px;
  border-radius: 4px;
  padding: 4px 0;
  left: auto;
  right: 4px;
}

/* Links inside the dropdown */
.dropdown-content a {
  color: white;
  padding: 6px 10px;
  text-decoration: none;
  display: block;

}

/* Change color of dropdown links on hover */
.dropdown-content a:hover {
  background-color: #666666;
}

/* Show the dropdown menu on hover */
.dropdown:hover .dropdown-content {
  display: block;
}
</style>