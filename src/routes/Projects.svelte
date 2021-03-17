<section class="section proj" id="projects">
  <div class="proj_el" id="proj1">
    <div class="proj_wrap">
      <img class="proj_img" src="./images/yoga.png" />
      <div class="proj_overlay">
        <div class="proj_title">Ashtanga Yoga</div>
        <p class="proj_descr">
          Mobile app guide to ashtanga yoga series and asanas.
        </p>
        <div class="proj_tags">#ReactNative #Expo</div>
      </div>
    </div>
  </div>
  <div class="proj_el" id="proj2">
    <div class="proj_wrap">
      <img class="proj_img" src="./images/hey.png" />
      <div class="proj_overlay">
        <div class="proj_title">Hey</div>
        <p class="proj_descr">
          Social mobile app guide for meeting people close to you.
        </p>
        <div class="proj_tags">#ReactNative #Expo #MobX #Firebase #Sentry</div>
      </div>
    </div>
  </div>
  <div class="proj_el" id="proj3">
    <div class="proj_wrap">
      <img class="proj_img" src="./images/beauty.png" />
      <div class="proj_overlay">
        <div class="proj_title">Beauty page template</div>
        <p class="proj_descr">Front-end web templete for beauty salon.</p>
        <div class="proj_tags">
          #JavaScript #ES6 #Pug #Sass #Gulp #GreenSock #ScrollMagic
        </div>
      </div>
    </div>
  </div>
  <div class="proj_el" id="proj4">
    <div class="proj_wrap">
      <img class="proj_img" src="./images/votex.png" />
      <div class="proj_overlay">
        <div class="proj_title">Votex</div>
        <p class="proj_descr">NodeJS app for poll creation.</p>
        <div class="proj_tags">#NodeJS #Pug #CSS #ChartJS #Heroku #MongoDB</div>
      </div>
    </div>
  </div>
</section>

<style type="text/scss">
  .proj {
    position: relative;
    font-size: 0;

    &_img {
      width: 100%;
    }

    &_overlay {
      width: 100%;
      max-height: 85px;
      padding: 30px;
      position: absolute;
      bottom: -10px;
      left: 0;
      backface-visibility: hidden;
      background: linear-gradient(to top, black 0%, transparent 100%);
      transition: max-height 0.5s ease-in-out;
    }

    &_title {
      font-weight: 400;
      font-size: 30px;
      color: white;
      width: 100%;
    }

    &_descr {
      font-size: 18px;
      color: white;
      margin-top: 20px;
    }

    &_wrap {
      overflow: hidden;
    }

    &_el {
      display: inline-block;
      vertical-align: top;
      margin-bottom: 100px;
      position: relative;
      width: 60%;
      overflow: hidden;

      &:nth-child(even) {
        float: right;
      }

      &:hover {
        .proj_overlay {
          max-height: 250px;
        }
      }
    }

    &_tags {
      font-size: 18px;
      color: white;
      margin-bottom: 30px;
      margin-top: 5px;
      font-weight: 600;
    }
  }

  @media screen and (max-width: 1200px) {
    .proj {
      &_title {
        font-size: 25px;
      }
    }
  }

  @media screen and (max-width: 500px) {
    .proj {
      display: block;

      &_el {
        width: 100%;
        margin-bottom: 50px;
      }

      &_overlay {
        max-height: 65px;
        padding: 20px;
      }

      &_title {
        font-size: 25px;
      }

      &_descr {
        font-size: 16px;
        color: white;
        margin-top: 10px;
      }

      &_tags {
        font-size: 16px;
        margin-bottom: 20px;
      }
    }
  }
</style>
