---
layout: archive
title: "Image Classifier"
permalink: /img_clf/
author_profile: true
---
{% include base_path %}

```html

<html>
<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.4/p5.js">
  
</script>
<script src="https://unpkg.com/ml5@1/dist/ml5.min.js">
  
</script>
<body>
<h2> Application of MobileNet and ml5.js</h2>
  
<div id="myResult">Scanning ...</div>
<img id="myImage" src="../files/pic 1.jpg" width="100%">


<script>
// A variable to hold the image we want to classify
let classifier;
let img;

// Initialize the Image Classifier method with MobileNet.
classifier = ml5.imageClassifier("MobileNet");
img = document.getElementById("myImage");
classifier.classify(img, gotResult);

// Callback function when classification has finished
function gotResult(results) {
  // Display the results
  let label = results[0].label;
  let confidence = (results[0].confidence * 100).toFixed(2);
  document.getElementById("myResult").innerHTML = label + "<br>Confidence: " + confidence + "%";
}
</script>
</body>
</html>

