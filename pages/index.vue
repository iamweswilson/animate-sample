<template>
  <div class="container mx-auto p-24 max-w-4xl">
      <h1 class="text-5xl">Sake for the elite</h1>
      <p>Tired of drinking the same sake normies drink? Of course you are, we all are. Your lips deserve sake that only the richest of the rich can drink. This is your lucky day.</p> 
      <p>Welcome to sake refined.</p>
      <canvas id="sake-spin" class="mt-20"></canvas>
      <p>
        That's right, this stuff is made of gold... well, it's actually made of rice, but it's as good as gold! Well, if gold were edible.
      </p>
      <p>
        You get the point
      </p>
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
h1 {
  color: white;
}
p {
  color: white;
  margin: 1rem 0;
}
canvas {
  /* position: fixed;
  left: 50%;
  top: 50%; */
  max-height: 100vh;
  max-width: 100vw;
  /* transform: translate(-50%, -50%); */
}
</style>
