# Swatch-Campus-Trash-Detection

## Problem Statement
We aim to provide the higher authorities responsible for sanitation and cleaning of large areas or intuitions a method for evaluation the work of their subordinates without manually inspecting the areas which might be kilometers apart.

## Solution
- Aerial Images taken using a drone will be inferred via a customyolov5 model which was trained on images of trash
- If the number of detections are more than a set threshold an alert is sent to the authorities in the form of an Incident in ServiceNow
- The inferred images are also stored in Amazon S3 with a reference of them in the database for reference
- The images corresponding to a given flight can be viewed via our Web Client

## Dronekit
- DroneKit is a python API for communicating with the ground station and UAV's which wraps over the ArduPilot API for flight control leveraging the MAVLINK protocol
- The Flight Controller we used (PixHawk) can communicate with the Onboard Computer as well as the Companion Computer on the drone.
- The Onboard Computer enables the drone to click pictures programmatically when a way point is hit
- Camera used: GoPro Hero 9 Black
- The Ground station connects to the main server with a WebSocket connection
  1. Its listens for LAUNCH command
  2. It broadcasts the location(Latitude and Longitude) in JSON format through websocket
- Tech Stack :- Ardupilot SITL,Dronekit SDK,Websockets using asyncio
- Website: [Swatch-Campus](https://sarvagnyadesh.github.io/Swatch-Campus)
![Screenshot 2023-03-29 080739](https://user-images.githubusercontent.com/120354771/228412366-9e120688-6767-4b08-9ff0-dc9917775ac4.png)
## Trash Detection Client
- On user demand the drone will sent images to the TDC.
  1. First the drone will upload the images to the FireBase.
  2. TDC will retrive the images from firebase and store them.
- After the images are successfully stored, TDC will start detection on them.
  - The model we used for detection is YOLO-v4.
- Once the detection is completed the detected images are uploded back to the firebase.
- The Website will take the images from there and display it to the end user
- [CODES](https://github.com/SarvagnyaDesh/Swatch-Campus-TDC)
