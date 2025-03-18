 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Video Slider with Thumbnails</title>
  <link href="https://unpkg.com/video.js/dist/video-js.min.css" rel="stylesheet">
  <script src="https://unpkg.com/video.js/dist/video.min.js"></script>
  <style type="text/css">
    /* General styling */
    .P1S6Video {
      position: relative;
      background-color: #f8f7f2;
      padding: 10px;
      display: flex;
      justify-content: center;
      margin: auto;
      align-content: center;
      align-items: center;
    }
    .video-js {
      width: 100%;
      height: 33vw;
      background: #f8f7f2;
    }
    .vjs-control-bar {
      display: none !important;
    }
    .slider {
      width: 60%;
      position: relative;
    }
    .video-container {
      display: none;
    }
    .video-container.active {
      display: block;
    }
    #prevBtn, #nextBtn {
      position: absolute;
      top: 42%;
      width: 60px;
      height: 80px;
      background: transparent;
      border: none;
      outline: 0;
      cursor: pointer;
      fill: #ffc90d;
    }
    #prevBtn {
      left: 5%;
    }
    #nextBtn {
      right: 5%;
    }
    /* Thumbnails section */
    .thumbnails {
      display: flex;
      justify-content: center;
      margin-top: 15px;
      gap: 10px;
    }
    .thumbnail {
      width: 80px;
      height: 50px;
      cursor: pointer;
      border: 2px solid transparent;
      transition: border 0.3s ease;
    }
    .thumbnail.active {
      border-color: #ffc90d;
    }
  </style>
</head>
<body>

<div class="P1S6Video">
  <!-- Previous button -->
  <button id="prevBtn">
    <svg xmlns="http://www.w3.org/2000/svg" width="60" height="80" viewBox="-10 -5 60 90"><polyline fill="none" stroke="#ffc90d" stroke-width="6" stroke-linecap="round" stroke-linejoin="round" points="25.63, 75.8 0.375, 38.087 25.63, 0.5"/></svg>
  </button>

  <div class="slider">
    <!-- Video 1 -->
    <div class="video-container active">
      <video id="video1" class="video-js" controls preload="auto" poster="https://spectrumbpo.com/wp-content/uploads/2024/11/BeanVivo-Poster.jpg">
        <source src="https://spectrumbpo.com/wp-content/uploads/2024/11/BeenVivo-Vid-1.mp4" type="video/mp4" />
      </video>
    </div>
    <!-- Video 2 -->
    <div class="video-container">
      <video id="video2" class="video-js" controls preload="auto" poster="https://spectrumbpo.com/wp-content/uploads/2024/11/BeanVivo-Poster.jpg">
        <source src="https://spectrumbpo.com/wp-content/uploads/2024/11/BeenVivo-Vid-2.mp4" type="video/mp4" />
      </video>
    </div>
    <!-- Video 3 -->
    <div class="video-container">
      <video id="video3" class="video-js" controls preload="auto" poster="https://spectrumbpo.com/wp-content/uploads/2024/11/BeanVivo-Poster.jpg">
        <source src="https://spectrumbpo.com/wp-content/uploads/2024/11/BeenVivo-Vid-3.mp4" type="video/mp4" />
      </video>
    </div>
    <!-- Video 4 -->
    <div class="video-container">
      <video id="video4" class="video-js" controls preload="auto" poster="https://spectrumbpo.com/wp-content/uploads/2024/11/BeanVivo-Poster.jpg">
        <source src="https://spectrumbpo.com/wp-content/uploads/2024/11/BeenVivo-Vid-4.mp4" type="video/mp4" />
      </video>
    </div>
    <!-- Thumbnails -->
    <div class="thumbnails" id="thumbnailsContainer"></div>
  </div>

  <!-- Next button -->
  <button id="nextBtn">
    <svg xmlns="http://www.w3.org/2000/svg" width="60" height="80" viewBox="-5 -6 60 90"><polyline fill="none" stroke="#ffc90d" stroke-width="6" stroke-linecap="round" stroke-linejoin="round" points="25.63, 75.8 50.875, 38.087 25.63, 0.5"/></svg>
  </button>
</div>

<script>
  const videoContainers = document.querySelectorAll('.video-container');
  const prevBtn = document.getElementById('prevBtn');
  const nextBtn = document.getElementById('nextBtn');
  const thumbnailsContainer = document.getElementById('thumbnailsContainer');
  let currentIndex = 0;

  // Create thumbnail navigation
  function createThumbnails() {
    videoContainers.forEach((_, i) => {
      const thumbnail = document.createElement('img');
      thumbnail.src = `https://spectrumbpo.com/wp-content/uploads/2024/11/BeanVivo-Poster.jpg`; // Adjust URLs for actual thumbnails
      thumbnail.classList.add('thumbnail');
      if (i === 0) thumbnail.classList.add('active');
      thumbnail.addEventListener('click', () => showVideo(i));
      thumbnailsContainer.appendChild(thumbnail);
    });
  }

  // Update thumbnails to highlight the active one
  function updateThumbnails(index) {
    const thumbnails = document.querySelectorAll('.thumbnail');
    thumbnails.forEach((thumb, i) => thumb.classList.toggle('active', i === index));
  }

  // Show the selected video
  function showVideo(index) {
    videoContainers.forEach((container, i) => {
      container.classList.toggle('active', i === index);
      const player = videojs(`video${i + 1}`);
      if (i === index) {
        player.play();
      } else {
        player.pause();
      }
    });
    updateThumbnails(index);
    currentIndex = index;
  }

  // Navigate videos with prev and next buttons
  prevBtn.addEventListener('click', () => {
    currentIndex = (currentIndex - 1 + videoContainers.length) % videoContainers.length;
    showVideo(currentIndex);
  });

  nextBtn.addEventListener('click', () => {
    currentIndex = (currentIndex + 1) % videoContainers.length;
    showVideo(currentIndex);
  });

  // Initialize video players and create thumbnails
  videoContainers.forEach((_, i) => videojs(`video${i + 1}`));
  createThumbnails();
</script>

</body>
</html>
