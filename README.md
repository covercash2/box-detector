A simple prototype for an object detection app.
The app should be a single Activity/screen that displays a camera viewport with graphical overlays for object detection.

The binary models and test data are not included in this repo.

## Image detection with Tensorflow lite

This app uses the Tensorflow 2 Image Classification to generate a model that is encoded as a Tensorflow lite model to be used on mobile (specifically Android).

The model is then uploaded to the Android app (./see) for use in object detection.

# Training the Model

Training for the model can be done in Google Colab with `model_maker_image_classification.ipyb` file.
The the jupyter notebook expects a `upload.zip` file containing images in a directory structure with a root directory named "labeled", e.g.:

```
!unzip /content/upload.zip
image_path = "/content/labeled"
```

The subdirectories in `/content/labeled` represent the associated labels, and their contents are the labeled images.
The notebook is taken directly from a Tensorflow example, so much of the code is basically dead after the "Detailed Process" header. (TODO cleanup)
Running the cells up to that point, however, will produce a model and ask to export it to Google Drive with the name `cereal_model.tflite`.
That model can then be added to the Android project for deployment.

# Build and Run

Once you have the trained model, the model must be uploaded to the `see/app/src/main/assets/custom_models` directory (TODO host the model and download it with gradle).
The Android app can then be built as normal (you may need to set the build variant to "debug" or else generate a signing key).
