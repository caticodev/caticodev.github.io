<script lang="ts">
  import { gsap } from "gsap";
  import { onMount } from "svelte";

  const intro = gsap.timeline();
  const mouseEnter = gsap.timeline({ paused: true });
  const mouseLeave = gsap.timeline({ paused: true });
  const mobile = window.innerWidth < 769;

  const load: gsap.TweenVars = {
    delay: 1,
    opacity: 1,
    ease: "circ.in",
    stagger: {
      amount: 1,
      from: "random",
      repeat: 3,
    },
  };
  const explode = (
    side: "left" | "right",
    first: boolean = false,
    scaled: boolean = false
  ): gsap.TweenVars => ({
    duration: 1,
    opacity: 0.8,
    ease: "expo.out",
    scale: `random(1,${scaled ? 5 : 10})`,
    x:
      side === "left"
        ? `random(-${scaled ? 100 : 500},${scaled ? 10 : 100})`
        : `random(${scaled ? 10 : 100},${scaled ? 100 : 500})`,
    ...(first ? { svgOrigin: "100 100" } : {}),
    ...(scaled && !first
      ? { repeatDelay: 2, repeat: -1, repeatRefresh: true }
      : {}),
  });
  const rotate = (loop: boolean = false) => ({
    duration: loop ? 30 : 3,
    rotation: loop ? 360 : 40,
    transformOrigin: "center center",
    ease: "none",
    ...(loop ? { repeat: -1 } : {}),
  });
  const implode = {
    duration: 0.5,
    x: 0,
    scale: 1,
    opacity: 1,
    ease: "expo.out",
  };
  const cleanRotation = {
    duration: 0.5,
    rotation: "0_short",
    transformOrigin: "center center",
    ease: "expo.out",
  };
  const scaleUp = {
    duration: 0.5,
    scale: mobile ? 2 : 3,
    x: mobile ? 0 : -230,
    y: mobile ? -100 : 0,
    ease: "expo.out",
  };

  onMount(() => {
    const paths = [...document.querySelectorAll(".logo path")];
    const left = [...document.querySelectorAll(".logo .left .shape")];
    const right = [...document.querySelectorAll(".logo .right .shape")];
    const wrapper = document.querySelector(".logo_wrapper");

    const addListeners = () => {
      let timeout;
      wrapper.addEventListener("mouseenter", () => {
        clearTimeout(timeout);
        timeout = setTimeout(() => {
          if (!mouseEnter.paused()) return;
          mouseLeave.pause();
          mouseEnter.play(0);
        }, 200);
      });
      wrapper.addEventListener("mouseleave", () => {
        clearTimeout(timeout);
        timeout = setTimeout(() => {
          if (!mouseLeave.paused()) return;
          mouseEnter.pause();
          mouseLeave.play(0);
        }, 200);
      });
    };

    intro
      .fromTo(paths, { opacity: 0 }, load, "loading")
      .addLabel("explode", "-=0.1")
      .to(left, explode("left", true), "explode")
      .to(right, explode("right", true), "explode")
      .addLabel("spin", "-=0.6")
      .to(paths, rotate(), "spin")
      .to(left, explode("left"), "spin+=1")
      .to(right, explode("right"), "spin+=1")
      .addLabel("outro", "-=0.2")
      .to([...left, ...right], implode, "outro")
      .to(paths, cleanRotation, "outro")
      .to(".logo_wrapper", scaleUp, "outro")
      .from(".intro_title, .intro_subtitle", {
        y: 30,
        opacity: 0,
        ease: "expo.out",
        stagger: {
          amount: 1.5,
        },
      })
      .from(
        ".contact",
        {
          opacity: 0,
          duration: 0.4,
          ease: "expo.in",
        },
        "-=0.25"
      )
      .call(addListeners);

    mouseEnter
      .addLabel("explode")
      .to(left, explode("left", true, true), "explode")
      .to(right, explode("right", true, true), "explode")
      .addLabel("spin", "-=0.6")
      .to(paths, rotate(true), "spin")
      .to(left, explode("left", false, true), "spin+=1")
      .to(right, explode("right", false, true), "spin+=1");

    mouseLeave
      .addLabel("outro")
      .to([...left, ...right], implode, "outro")
      .to(paths, cleanRotation, "outro");
  });
</script>

<div class="logo">
  <div class="logo_wrapper">
    <svg
      width="200"
      height="200"
      viewBox="0 0 200 200"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
    >
      <defs>
        <filter id="polycleaner" color-interpolation-filters="sRGB">
          <feComponentTransfer>
            <feFuncA type="table" tableValues="0 0.5 1 1" />
          </feComponentTransfer>
        </filter>
      </defs>
      <g class="left">
        <g class="shape"
          ><path
            d="M29.3214 0.378296L73.5821 56.5192L100.099 46.6L29.3214 0.378296Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M49.0945 56.3891L73.5811 56.5192L29.3224 0.378296L49.0945 56.3891Z"
            fill="#1B1B1B"
          /></g
        >
        <g class="shape"
          ><path
            d="M29.3214 0.378296L10.8587 83.7458L49.0945 56.3891L29.3214 0.378296Z"
            fill="#2B2B2B"
          /></g
        >
        <g class="shape"
          ><path
            d="M0.122002 83.3576L10.8583 83.7458L29.323 0.378296L0.122002 83.3576Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M0.122002 83.3577L13.3469 97.4897L10.8593 83.7458L0.122002 83.3577Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M49.0945 56.3892L64.5463 104.621L73.5811 56.5192L49.0945 56.3892Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M10.8587 83.7458L64.5463 104.621L49.0935 56.3892L10.8587 83.7458Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M13.3463 97.4897L64.5463 104.621L10.8587 83.7458L13.3463 97.4897Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M35.2139 120.049L64.5463 104.621L13.3463 97.4896L35.2139 120.049Z"
            fill="#5A5A5A"
          /></g
        >
        <g class="shape"
          ><path
            d="M64.5463 104.621L100.098 46.601L73.5811 56.5192L64.5463 104.621Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M13.3463 97.4896L23.4289 131.588L35.2139 120.049L13.3463 97.4896Z"
            fill="#2B2B2B"
          /></g
        >
        <g class="shape"
          ><path
            d="M52.1065 135.608L64.5463 104.621L35.2139 120.049L52.1065 135.608Z"
            fill="#5A5A5A"
          /></g
        >
        <g class="shape"
          ><path
            d="M23.4289 131.589L52.1055 135.609L35.2139 120.049L23.4289 131.589Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M23.4289 131.589L38.0955 153.5L52.1055 135.609L23.4289 131.589Z"
            fill="#1B1B1B"
          /></g
        >
        <g class="shape"
          ><path
            d="M75.4139 154.408L64.5473 104.621L52.1075 135.608L75.4139 154.408Z"
            fill="#5A5A5A"
          /></g
        >
        <g class="shape"
          ><path
            d="M75.4139 154.408L100.032 155.575L64.5473 104.621L75.4139 154.408Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M100.032 155.575L100.098 46.6L64.5453 104.621L100.032 155.575Z"
            fill="#1B1B1B"
          /></g
        >
        <g class="shape"
          ><path
            d="M47.1304 166.336L52.1055 135.608L38.0955 153.501L47.1304 166.336Z"
            fill="#1B1B1B"
          /></g
        >
        <g class="shape"
          ><path
            d="M47.1303 166.336L75.4139 154.408L52.1065 135.608L47.1303 166.336Z"
            fill="#1B1B1B"
          /></g
        >
        <g class="shape"
          ><path
            d="M47.1303 166.336L67.5582 167.763L75.4139 154.408L47.1303 166.336Z"
            fill="#2B2B2B"
          /></g
        >
        <g class="shape"
          ><path
            d="M47.1303 166.336L59.0458 179.821L67.5572 167.763L47.1303 166.336Z"
            fill="#5A5A5A"
          /></g
        >
        <g class="shape"
          ><path
            d="M75.4139 154.408L100.032 181.117V155.575L75.4139 154.408Z"
            fill="#5A5A5A"
          /></g
        >
        <g class="shape"
          ><path
            d="M67.5572 167.763L100.032 181.117L75.4149 154.408L67.5572 167.763Z"
            fill="#1B1B1B"
          /></g
        >
        <g class="shape"
          ><path
            d="M100.032 181.117L89.1632 199.009L99.9722 191.699L100.032 181.117Z"
            fill="#5A5A5A"
          /></g
        >
        <g class="shape"
          ><path
            d="M67.5572 167.763L89.1632 199.01L100.032 181.117L67.5572 167.763Z"
            fill="#1B1B1B"
          /></g
        >
        <g class="shape"
          ><path
            d="M59.0458 179.821L89.1632 199.01L67.5572 167.763L59.0458 179.821Z"
            fill="#1B1B1B"
          /></g
        >
        <g class="shape"
          ><path
            d="M89.1642 199.01H100.032V191.67L89.1642 199.01Z"
            fill="#2B2B2B"
          /></g
        >
      </g>
      <g class="right">
        <g class="shape"
          ><path
            d="M170.681 0.395081L126.422 56.536L99.9045 46.6168L170.681 0.395081Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M150.907 56.4059L126.421 56.536L170.681 0.394104L150.907 56.4059Z"
            fill="#1B1B1B"
          /></g
        >
        <g class="shape"
          ><path
            d="M170.681 0.395081L189.144 83.7635L150.907 56.4059L170.681 0.395081Z"
            fill="#2B2B2B"
          /></g
        >
        <g class="shape"
          ><path
            d="M199.881 83.3744L189.144 83.7636L170.681 0.394104L199.881 83.3744Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M199.881 83.3744L186.657 97.5064L189.144 83.7626L199.881 83.3744Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M150.907 56.4059L135.457 104.637L126.422 56.5359L150.907 56.4059Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M189.144 83.7635L135.457 104.637L150.907 56.4059L189.144 83.7635Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M186.657 97.5074L135.457 104.637L189.144 83.7635L186.657 97.5074Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M164.788 120.066L135.457 104.637L186.656 97.5063L164.788 120.066Z"
            fill="#5A5A5A"
          /></g
        >
        <g class="shape"
          ><path
            d="M135.457 104.637L99.9045 46.6177L126.422 56.536L135.457 104.637Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M186.657 97.5073L176.573 131.606L164.788 120.066L186.657 97.5073Z"
            fill="#2B2B2B"
          /></g
        >
        <g class="shape"
          ><path
            d="M147.897 135.626L135.457 104.637L164.788 120.066L147.897 135.626Z"
            fill="#5A5A5A"
          /></g
        >
        <g class="shape"
          ><path
            d="M176.573 131.606L147.897 135.626L164.788 120.066L176.573 131.606Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M176.573 131.606L161.906 153.517L147.897 135.626L176.573 131.606Z"
            fill="#1B1B1B"
          /></g
        >
        <g class="shape"
          ><path
            d="M124.587 154.425L135.457 104.637L147.897 135.625L124.587 154.425Z"
            fill="#5A5A5A"
          /></g
        >
        <g class="shape"
          ><path
            d="M124.587 154.425L99.9702 155.592L135.457 104.637L124.587 154.425Z"
            fill="#CCCCCC"
          /></g
        >
        <g class="shape"
          ><path
            d="M99.9702 155.592L99.9045 46.6168L135.457 104.637L99.9702 155.592Z"
            fill="#1B1B1B"
          /></g
        >
        <g class="shape"
          ><path
            d="M152.872 166.353L147.897 135.625L161.906 153.517L152.872 166.353Z"
            fill="#1B1B1B"
          /></g
        >
        <g class="shape"
          ><path
            d="M152.872 166.353L124.588 154.425L147.897 135.625L152.872 166.353Z"
            fill="#1B1B1B"
          /></g
        >
        <g class="shape"
          ><path
            d="M152.872 166.353L132.444 167.779L124.588 154.425L152.872 166.353Z"
            fill="#2B2B2B"
          /></g
        >
        <g class="shape"
          ><path
            d="M152.872 166.353L140.956 179.837L132.445 167.779L152.872 166.353Z"
            fill="#5A5A5A"
          /></g
        >
        <g class="shape"
          ><path
            d="M124.587 154.425L99.9702 181.134V155.592L124.587 154.425Z"
            fill="#5A5A5A"
          /></g
        >
        <g class="shape"
          ><path
            d="M132.445 167.779L99.9702 181.134L124.587 154.425L132.445 167.779Z"
            fill="#1B1B1B"
          /></g
        >
        <g class="shape"
          ><path
            d="M99.9702 181.133L110.839 199.027L99.9702 191.717V181.133Z"
            fill="#5A5A5A"
          /></g
        >
        <g class="shape"
          ><path
            d="M132.445 167.779L110.839 199.027L99.9702 181.134L132.445 167.779Z"
            fill="#1B1B1B"
          /></g
        >
        <g class="shape"
          ><path
            d="M140.955 179.837L110.839 199.027L132.445 167.779L140.955 179.837Z"
            fill="#1B1B1B"
          /></g
        >
        <g class="shape"
          ><path
            d="M110.839 199.027H99.9702V191.687L110.839 199.027Z"
            fill="#2B2B2B"
          /></g
        >
      </g>
    </svg>
  </div>
</div>

<style type="text/scss">
  .logo {
    position: absolute;
    z-index: 5;
    width: 100vw;
    height: 100vh;
    top: 0;
    left: 0;

    &_wrapper {
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%);
    }

    svg {
      overflow: visible;
      width: 100px;
      height: 100px;
      filter: url(#polycleaner);
    }
  }
</style>
