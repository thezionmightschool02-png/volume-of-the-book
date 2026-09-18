# The Zion Might — 42s Website Promo Integration

## Files
- `zion_might_42s_promo_github.mp4` — 1920×1080 web-ready promo with voiceover + cinematic background audio.
- `zion_might_website_poster.jpg` — poster/thumbnail from the older-community/book scene (around 33.5s), chosen to make the section visually inviting.

## Recommended placement
Replace the existing promotional image in the relevant Volume of the Book / Path of Life section with the video below.

## HTML
```html
<div class="zion-promo-wrap">
  <video
    id="zionPromo"
    class="zion-promo-video"
    preload="metadata"
    poster="assets/zion_might_website_poster.jpg"
    playsinline
    muted
    loop
    controls
    aria-label="The Zion Might — Volume of the Book promotional video">
    <source src="assets/zion_might_42s_promo_github.mp4" type="video/mp4">
    Your browser does not support HTML5 video.
  </video>
</div>
```

## CSS
```css
.zion-promo-wrap {
  width: 100%;
  max-width: 1100px;
  margin: 0 auto;
  border-radius: 18px;
  overflow: hidden;
  box-shadow: 0 18px 50px rgba(0,0,0,.20);
}

.zion-promo-video {
  display: block;
  width: 100%;
  height: auto;
  aspect-ratio: 16 / 9;
  object-fit: cover;
  background: #000;
  cursor: pointer;
}
```

## Autoplay-on-scroll + tap-for-sound
```html
<script>
(() => {
  const video = document.getElementById('zionPromo');
  if (!video) return;

  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        video.muted = true;
        video.play().catch(() => {});
      } else {
        video.pause();
      }
    });
  }, { threshold: 0.45 });

  observer.observe(video);

  video.addEventListener('click', () => {
    if (video.paused) video.play().catch(() => {});
    video.muted = !video.muted;
  });
})();
</script>
```

### Why this setup
- Starts automatically when the visitor reaches the section, while muted for browser autoplay compatibility.
- Tapping/clicking the video turns the voiceover/music on.
- The poster shows a human/community/book moment rather than the heaven imagery, so the first impression is people + the Volume of the Book.
- `playsinline` keeps mobile playback inside the page.
- The web-ready MP4 is kept at 1920×1080 while compressed enough to be practical for a GitHub Pages site.

## Asset paths
Put both files in the same asset folder used by the site, then adjust the two `src`/`poster` paths if your existing project uses a different folder.
