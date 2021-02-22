<template>
  <div class="container text-center mx-auto p-24">
      <canvas id="sake-spin"></canvas>
  </div>
</template>

<script>
export default {
  mounted() {
    const html = document.documentElement;
    const canvas = document.getElementById("sake-spin");
    const context = canvas.getContext("2d");

    const frameCount = 38;
    const currentFrame = index => (
      `/img/test/test0${index.toString().padStart(4, '0')}.jpg`
    )

    const preloadImages = () => {
      for (let i = 1; i < frameCount; i++) {
        const img = new Image();
        img.src = currentFrame(i);
      }
    };

    const img = new Image()
    img.src = currentFrame(1);
    canvas.width=800;
    canvas.height=1067;
    img.onload=function(){
      context.drawImage(img, 0, 0);
    }

    const updateImage = index => {
      img.src = currentFrame(index);
      context.drawImage(img, 0, 0);
    }

    window.addEventListener('scroll', () => {
      const scrollTop = html.scrollTop;
      const maxScrollTop = html.scrollHeight - window.innerHeight;
      const scrollFraction = scrollTop / maxScrollTop;
      const frameIndex = Math.min(
        frameCount - 1,
        Math.ceil(scrollFraction * frameCount)
      );
      requestAnimationFrame(() => updateImage(frameIndex + 1))
    });
    preloadImages()
  }
}
</script>

<style>
html {
  height: 100vh;
}
body {
  background: #000;
  height: 500vh;
}
canvas {
  position: fixed;
  left: 50%;
  top: 50%;
  max-height: 100vh;
  max-width: 100vw;
  transform: translate(-50%, -50%);
  background: white;
}
</style>
