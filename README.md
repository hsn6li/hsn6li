<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Take a Photo</title>
</head>
<body>
    <h1>Click below to take a photo</h1>
    <video id="video" width="320" height="240" autoplay></video>
    <button id="snap">Take Photo</button>
    <canvas id="canvas" width="320" height="240"></canvas>
    <a id="download" download="photo.png">Download Photo</a>

    <script>
        const video = document.getElementById('video');

        // Access the camera
        if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
            navigator.mediaDevices.getUserMedia({ video: true }).then(function(stream) {
                video.srcObject = stream;
                video.play();
            });
        }

        // Elements for taking the snapshot
        const canvas = document.getElementById('canvas');
        const context = canvas.getContext('2d');
        const snap = document.getElementById('snap');
        const download = document.getElementById('download');

        snap.addEventListener('click', function() {
            // Draw the image on the canvas
            context.drawImage(video, 0, 0, 320, 240);

            // Convert the canvas content to a data URL (base64)
            const dataURL = canvas.toDataURL('image/png');

            // Set the href attribute of the download link to the data URL
            download.href = dataURL;
        });
    </script>
</body>
</html>
