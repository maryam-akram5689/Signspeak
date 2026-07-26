About SignSpeak
Live deployed app : https://signspeak-phi.vercel.app/
Public GitHub repository URL: https://github.com/maryam-akram5689/Signspeak
The Big Picture & Why I Built It
Communicating with someone who uses sign language shouldn't require an interpreter or expensive hardware. I built SignSpeak to help bridge the everyday communication gap between non-verbal or deaf individuals and the people around them—whether that's teachers, classmates, or shopkeepers.
Most existing sign language tools require downloading heavy desktop software, buying specialized gloves or sensors, or paying for pricey API subscriptions. SignSpeak runs 100% inside any web browser, even on basic Chromebooks and budget laptops. It uses your device’s built-in webcam to recognize hand gestures in real time, translate them into text on screen, and read them out loud.

How to Use the App (Step-by-Step)
Using SignSpeak is straightforward and requires zero technical setup:

1. Launch the App: Open the live link in any modern web browser (Google Chrome works best).
2. Allow Camera Access: When your browser asks for permission to use your webcam, click Allow. You'll see your camera feed appear on the screen within a few seconds.
3. Show Your Hand: Hold one hand up in front of the camera. You will instantly see small blue tracking dots appear over your joints and fingers—this shows that the AI is actively tracking your hand shape.
4. See Live Recognition: The app comes pre-trained with basic gestures (HELP, HELLO, YES, and NO). Put your hand into one of those gestures, and look at the Live Prediction box—it will display the recognized word in bright green!
5. Hear the Sign: Want the app to speak for you? Click the 🔊 Speak Word button at the bottom right, and your computer will read the predicted word out loud using text-to-speech.

What the App Can Do (Features List)
1. Real-Time Skeleton Tracking: Uses computer vision to map 21 key points on your hand in 3D space ($X, Y, Z$ coordinates) without lag.
2. Instant Gesture Classification: Translates raw finger positioning into plain English words within milliseconds.
3. Auto-Loading AI Dataset: Embedded pre-trained gesture data means you don't have to train signs from scratch every time you open the app.
4. Custom Gesture Recording: Interactive training buttons let you record new hand signs or reinforce existing ones on the fly.
5. Text-to-Speech Engine: Built-in audio synthesis speaks the recognized sign aloud for auditory communication.
6. Export & Import Models: Lets you save your trained gesture dataset as a lightweight .json file and reload it anytime.
7. Zero Installation & Privacy-Friendly: Runs completely on the client side inside the browser—no video or personal data is ever sent to an external server.

How I Trained the AI Model
Training a gesture recognition model right inside the browser was one of the most interesting parts of this project! Here is how the training process works behind the scenes:

1. Spatial Coordinate Extraction (MediaPipe)
Instead of training a heavy image-recognition model on entire camera frames (which takes a lot of processing power and can get confused by background clutter), I used MediaPipe Hands. Whenever a hand is shown to the camera, MediaPipe pinpoints 21 joint locations (fingertips, knuckles, wrist) and extracts their precise 3D spatial coordinates ($X, Y, Z$). This condenses the complex hand shape into a lightweight list of 63 numbers.

2. Gesture Learning via KNN (K-Nearest Neighbors)
To classify those coordinate lists into actual words, I paired TensorFlow.js with a K-Nearest Neighbors (KNN) classifier:

Recording Samples: When you hold up a hand gesture (like a thumbs-up for "YES") and click Record "YES", the app takes those 63 coordinate numbers and tags them under the label "YES".

Pattern Recognition: By clicking the button 5 to 10 times while slightly shifting your hand position, the KNN classifier learns the spatial "fingerprint" of that specific sign.

Live Matching: When you show a sign to the camera during live prediction, the classifier measures the mathematical distance between your live hand coordinates and all recorded samples to instantly pick the closest matching gesture label.

3. Making It Permanent (Auto-Load & File Save)
Because browser memory resets when a tab is closed, I built custom save and load handlers:
The saveModel() function extracts the raw tensor dataset matrix from the classifier, converts it into a structured JSON file, and downloads it to your computer.
To make the app user-friendly out of the box, I embedded a copy of these pre-trained coordinate matrices directly into the app's JavaScript code. This way, the moment anyone opens the live link, the AI automatically loads the gestures without asking the user to upload anything.

Tools, Services, and AI Models Used
1. Frontend & Styling: HTML5, JavaScript (ES6+), Tailwind CSS (via CDN)
2. Vision Model: MediaPipe Hands (@mediapipe/hands)
3. Machine Learning Engine: TensorFlow.js (@tensorflow/tfjs)
4. Classification Model: KNN Classifier (@tensorflow-models/knn-classifier)
5. Audio Engine: Web Speech API (SpeechSynthesisUtterance)
6. Deployment & Hosting: GitHub + Vercel

Screenshots of the App in Action:
https://github.com/maryam-akram5689/Signspeak/blob/main/Screenshot%20(366).png
https://github.com/maryam-akram5689/Signspeak/blob/main/Screenshot%20(367).png
https://github.com/maryam-akram5689/Signspeak/blob/main/Screenshot%20(368).png
https://github.com/maryam-akram5689/Signspeak/blob/main/Screenshot%20(369).png

