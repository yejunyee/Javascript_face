# 디지털 영상처리 퀴즈 코드
p5js로 구현
~~~js
let faceapi;
let video;
let detections;
 
// by default all options are set to true
const detectionOptions = {
withLandmarks: true,
withDescriptors: false,
minConfidence: 0.5,
   MODEL_URLS: {
        //Mobilenetv1Model: 'https://raw.githubusercontent.com/ml5js/ml5-data-and-models/main/models/faceapi/ssd_mobilenetv1_model-weights_manifest.json',
        FaceLandmarkModel: 'https://raw.githubusercontent.com/ml5js/ml5-data-and-models/main/models/faceapi/face_landmark_68_model-weights_manifest.json',
        //FaceLandmark68TinyNet: 'https://raw.githubusercontent.com/ml5js/ml5-data-and-models/main/models/faceapi/face_landmark_68_tiny_model-weights_manifest.json',
        //FaceRecognitionModel: 'https://raw.githubusercontent.com/ml5js/ml5-data-and-models/main/models/faceapi/face_recognition_model-weights_manifest.json',
    },
};
 
function setup() {
    createCanvas(360,270);
 
    // load up your video
    video = createCapture(VIDEO);
    video.size(width, height);
 
    // video.hide(); // Hide the video element, and just show the canvas
    faceapi = ml5.faceApi(video, detectionOptions, modelReady);
    textAlign(RIGHT);
 
}
 
 
function draw() {
 
}

function modelReady() {
    console.log("ready!");
    console.log(faceapi);
    faceapi.detect(gotResults);
}
 
 
function gotResults(err, result) {
    if (err) {
        console.log(err);
        return;
    }
 
    // console.log(result)
    detections = result;
 
    // background(220);
    background(255);
    image(video, 0, 0, width, height);
 
    if (detections) {
        if (detections.length > 0) {
            // console.log(detections)
            // 요기서 얼굴에 관련된 그림을 그리는 코드 
          drawBox(detections);
          text="예준";
        }
    }
 
    faceapi.detect(gotResults);
}


function drawBox(detections) {
    for (let i = 0; i < detections.length; i += 1) {
        const alignedRect = detections[i].alignedRect;
        const x = alignedRect._box._x;
        const y = alignedRect._box._y;
        const boxWidth = alignedRect._box._width;
        const boxHeight = alignedRect._box._height;

        noFill();
        stroke(161, 95, 251);
        strokeWeight(2);
        rect(x, y, boxWidth, boxHeight);
    }
}
~~~
index.html 파일에 코드 추가

    <script src="https://unpkg.com/ml5@0.5.0/dist/ml5.min.js" type="text/javascript"></script>







