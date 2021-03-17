<section class="section intro" id="intro">
  <div class="intro_text">
    <h1 class="intro_title">catico</h1>
    <div>
      <div class="intro_subtitle">developer.&nbsp;</div>
      <div class="intro_subtitle">designer.&nbsp;</div>
      <div class="intro_subtitle">maker.</div>
    </div>
  </div>
</section>

<style type="text/scss">
  .intro {
    min-height: 500px;
    height: 100vh;
    overflow: hidden;
    position: relative;

    &_title {
      font-size: 128px;
      color: var(--title);
      font-weight: 100;
    }

    &_subtitle {
      display: inline-block;
      font-size: 40px;
      color: var(--text);
      font-weight: 200;
    }

    &_text {
      position: absolute;
      top: 50%;
      left: 47%;
      transform: translateY(-50%);
      margin-top: -20px;
    }
  }

  @media screen and (max-width: 1200px) {
    .intro {
      &_title {
        font-size: 90px;
      }

      &_subtitle {
        font-size: 32px;
      }
    }
  }

  @media screen and (max-width: 900px) {
    .intro {
      &_text {
        left: 50%;
        transform: translate(-50%, -50%);
        margin-top: 150px;
        text-align: center;
        width: 100%;
      }
    }
  }

  @media screen and (max-width: 500px) {
    .intro {
      &_title {
        font-size: 4em;
      }

      &_subtitle {
        font-size: 1.5em;
      }

      &_text {
        margin-top: 100px;
      }
    }
  }
</style>
