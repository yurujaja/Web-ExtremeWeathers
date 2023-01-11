<template>
  <div class="cover">
    <div class="callout">
      <!-- <h1>Global trade</h1> -->
      <h2 class="cover-title">
        Extreme Climate and Weather<br />
        <small></small>
      </h2>
    </div>
  </div>
</template>

<script>
export default {
  name: "CoverPage",
};
</script>

<style scoped>
.cover {
  background-image: url("../../../public/images/cover.gif");
  background-repeat: no-repeat;
  background-size: 100vw;
  background-attachment: fixed;
  /*background-size: cover;*/

  height: 500px;
  width: 100vw;
}

.callout {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100%;
  text-align: center;
  position: relative;
  z-index: 10;
  width: 70%;
  margin: auto;
  /*@media (max-width: 767px) {*/
  /*  width: 90%;*/
  /*}*/
}

.cover-title {
  text-align: center;
  font-weight: bold;
  color: #ffffff;
  /* width: 50%; */
  min-width: 375px;
  margin: auto;
}
</style>
