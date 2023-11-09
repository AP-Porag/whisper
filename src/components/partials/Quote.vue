<template>
  <div class="blog_post">
    <div class="img_pod">
      <img src="https://pbs.twimg.com/profile_images/890901007387025408/oztASP4n.jpg" alt="random image">
    </div>
    <div class="container_copy">
      <h3>12 January 2019</h3>
      <h1>CSS Positioning</h1>
      <p>The position property specifies the type of positioning method used for an element (static, relative, absolute, fixed, or sticky).</p>
    </div>

  </div>
</template>

<script>
export default {
  name: "Quote"
}
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css?family=Roboto:300,400,700&display=swap");

.blog_post {
  background: #fff;
  border-radius: 10px;
  box-shadow: 1px 1px 2rem rgba(0, 0, 0, 0.3);
  position: relative;
}


.container_copy {
  //padding: 6rem 4rem 0px 4rem;
  padding: 4rem 4rem 0px 4rem;
}

.img_pod {
  height: 110px;
  width: 110px;
  background: linear-gradient(90deg, #ff9966, #ff5e62);
  z-index: 10;
  box-shadow: 1px 1px 2rem rgba(0, 0, 0, 0.3);
  border-radius: 100%;
  position: absolute;
  left: -10%;
  top: -13%;
  display: flex;
  align-items: center;
  justify-content: center;
}

img {
  height: 110px;
  width: 110px;
  position: relative;
  border-radius: 100%;
  box-shadow: 1px 1px 2rem rgba(0, 0, 0, 0.3);
  z-index: 1;
}

h3 {
  margin: 0 0 0.5rem 0;
  color: #999;
  font-size: 1.25rem;
}

h1 {
  margin: 0 0 1rem 0;
  font-size: 2.5rem;
  letter-spacing: 0.5px;
  color: #333;
}

p {
  margin: 0 0 4.5rem 0;
  font-size: 1.5rem;
  line-height: 1.45;
  color: #333;
}



</style>