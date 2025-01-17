---
layout: archive
title: "Image Classifier"
permalink: /img_clf/
author_profile: true
---
{% include base_path %}

```html
<html>
<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.4/p5.js"></script>
<script src="https://unpkg.com/ml5@1/dist/ml5.min.js"></script>
<body>
<h2>Application of MobileNet and ml5.js</h2>

<!-- Form to upload an image -->
<form id="uploadForm">
  <input type="file" id="imageUpload" accept="image/*">
  <input type="button" value="Upload Image" onclick="loadImage()">
</form>

<div id="myResult">Scanning ...</div>
<img id="myImage" src="" width="50%">

<!-- Button to classify the uploaded image -->
<input type="button" value="Classify Image" onclick="classifyImage()">

<script>
// Initialize the Image Classifier method with MobileNet.
classifier = ml5.imageClassifier("MobileNet");

// Function to load the uploaded image
function loadImage() {
  const input = document.getElementById('imageUpload').files[0];
  if (!input) return;

  const reader = new FileReader();
  reader.onload = function(e) {
    img = document.getElementById('myImage');
    img.src = e.target.result;
  }
  reader.onerror = function() {
    document.getElementById("myResult").innerHTML = "Error loading image.";
  }
  reader.readAsDataURL(input);
}

// Function to classify the loaded image
function classifyImage() {
  const img = document.getElementById('myImage');
  if (!img.src) {
    document.getElementById("myResult").innerHTML = "No image loaded.";
    return;
  }
  classifier.classify(img, gotResult);
}

// Callback function when classification has finished
function gotResult(error, results) {
  if (error) {
    document.getElementById("myResult").innerHTML = "Error classifying image.";
    return;
  }
  // Display the results
  let label = results[0].label;
  let confidence = (results[0].confidence * 100).toFixed(2);
  document.getElementById("myResult").innerHTML = label + "<br>Confidence: " + confidence + "%";
}
</script>
</body>
</html>
