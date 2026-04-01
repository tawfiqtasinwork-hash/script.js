// script.js

// Sample data for videos
const videos = [
    { id: 1, title: 'Video 1', category: 'Tech', url: 'video1.mp4' },
    { id: 2, title: 'Video 2', category: 'Travel', url: 'video2.mp4' },
    { id: 3, title: 'Video 3', category: 'Cooking', url: 'video3.mp4' },
];

// Function to generate video grid
function generateVideoGrid(category) {
    const videoContainer = document.getElementById('video-grid');
    videoContainer.innerHTML = '';

    const filteredVideos = category ? videos.filter(video => video.category === category) : videos;

    filteredVideos.forEach(video => {
        const videoElement = document.createElement('div');
        videoElement.className = 'video-item';
        videoElement.innerHTML = `
            <h3>${video.title}</h3>
            <video width='320' height='240' controls>
                <source src='${video.url}' type='video/mp4'>
                Your browser does not support the video tag.
            </video>
            <button onclick='openLightbox(${video.id})'>Watch</button>
        `;
        videoContainer.appendChild(videoElement);
    });
}

// Lightbox functionality
function openLightbox(videoId) {
    const video = videos.find(v => v.id === videoId);
    const lightbox = document.getElementById('lightbox');
    lightbox.style.display = 'block';
    const lightboxVideo = document.getElementById('lightbox-video');
    lightboxVideo.src = video.url;
}

function closeLightbox() {
    const lightbox = document.getElementById('lightbox');
    lightbox.style.display = 'none';
    const lightboxVideo = document.getElementById('lightbox-video');
    lightboxVideo.src = '';
}

// Event listener for category filter
document.getElementById('category-filter').addEventListener('change', (e) => {
    generateVideoGrid(e.target.value);
});

// Initialize video grid
window.onload = () => {
    generateVideoGrid();
};

// Lightbox close button event
document.getElementById('close-lightbox').addEventListener('click', closeLightbox);
