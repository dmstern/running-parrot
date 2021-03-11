<div class="loading__animation">
  <div></div>
  <div></div>
  <div></div>
</div>

<style>  
  .loading__animation {
    display: flex;
    width: 100px;
    justify-content: space-between;
    margin: 20px auto;
  }

  .loading__animation div {
    width: 20px;
    height: 20px;
    background-color: #5a4631;
    animation: load 900ms ease infinite;
  }

  .loading__animation div:nth-child(2) {
    animation-delay: 300ms;
  }

  .loading__animation div:nth-child(3) {
    animation-delay: 600ms;
  }

  @keyframes load {
    from {
      background-color: #1f1812;
    }
    
    to {
      background-color: #5a4631;
    }
  }

</style>