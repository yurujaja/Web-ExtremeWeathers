 <template>
    <div class="full-width">
      <div class="my-content">
        <slot></slot>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "LimitWidth"
  }
  </script>
  
  <style scoped>
  .full-width {
    width: 100vw;
    align-items: center;
    align-content: center;
    align-self: center;
    margin: auto;
    text-align: center;
  }
  
  .my-content {
    align-items: center;
    align-content: center;
    align-self: center;
    margin: auto;
    text-align: center;
  }
  
  @media (max-width: 699px) {
    .my-content {
      /*height: 100%;*/
      width: 100vw;
      /*max-width: 700px*/
    }
  }
  
  @media (min-width: 700px) and (max-width: 999px) {
    .my-content {
      /*height: 100%;*/
      width: 95vw;
      /*max-width: 700px*/
    }
  }
  
  /* Limit width on wide screen */
  @media (min-width: 1000px) and (max-width: 1199px) {
    .my-content {
      /*height: 100%;*/
      width: 90vw;
      max-width: 900px
    }
  }
  
  @media (min-width: 1200px) and (max-width: 1499px) {
    .my-content {
      /*height: 100%;*/
      width: 90vw;
      max-width: 1000px
    }
  }
  
  @media (min-width: 1500px) {
    .my-content {
      /*height: 100%;*/
      width: 90vw;
      max-width: 1200px
    }
  }
  
  </style>
  