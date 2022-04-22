# Classifier based Image Sorter
This app can use any number of image classifiers to detect any number of target labels, then sort those images into 1 of 2 folders if the target label is detected.

To edit, add, or remove models, be sure to use the appropriate [alwaysAI CLI commands](https://dashboard.alwaysai.co/docs/application_development/changing_the_model.html) to do so, in addition to adding a classifier record into the `alwaysai.app.json` file (see the Configuration section below).

## Requirements
- Sign up for [alwaysAI](https://dashboard.alwaysai.co/auth?register=true)
- Install [alwaysAI tooling](https://dashboard.alwaysai.co/docs/getting_started/development_computer_setup.html)

## Configuration
This app makes use of key-values in the `alwaysai.app.json` file for set up and variable assignments:

Key | Value Type | Description
-----| ---------- | ----------
scripts | dictionary | Required by alwaysAI's CLI to specify which file to run within a docker container
models | dictionary | Required by alwaysAI's CLI to determine which CV models to download and make available to the app's docker container
classifiers_needed_to_agree | float | Float representation of the minimum percent (100% = 1.0) of classifiers needed to make a determination if a target object was detected. So if 10 classifiers are used, a value of 0.2 here, would require at least 2 of the 10 classifiers to be in agreement before considering a target object found. Default is 0.5
detected_output_folder | string | Location from the app root folder to put images with target objects into. Default is `output_images/found`
empty_output_folder | string | Location from the app root folder to put images where no target objects were detected. Default is `output_images/not_found`
classifiers | array | An array of dictionaries with classifier information. See below for expected keys for each dictionary object

Classifier Information:

Key | Value Type | Description
-----| ---------- | ----------
model_id | string | The model id as found from [alwaysAI's Model Catalog](https://dashboard.alwaysai.co/model-catalog/models?category=Classification). Note that there should be a duplicate of this string value in the higher level 'models' key-value pair which is used by alwaysAI's CLI tool. To add or remove models for download, see [the docs here](https://dashboard.alwaysai.co/docs/application_development/changing_the_model.html)
confidence_level_threshold | float | Each model has a [confidence_level](https://dashboard.alwaysai.co/docs/reference/edgeiq.html#edgeiq.image_classification.ClassificationPrediction) value that's provided with each [classification prediction](https://dashboard.alwaysai.co/docs/reference/edgeiq.html#edgeiq.image_classification.ClassificationResults). Many models will use a float value from 0.0-1.0 with 1.0 = 100%, but some models may have a different value based system, like `squeezenet_v1.1`
target_labels | array of strings | List of all labels this model should be filtering / looking for. This will usually be a subset of all the available labels this model is capable of detecting. If no labels are specified nothing will be returned, in other words the `detected_output_folder` will be empty after processing

## Running
Use the alwaysAI CLI to build and start this app:
Build: `aai app install`
Run: `aai app start`
**NOTE: You can run this app remotely onto another device or build & run locally. Use `aai app configure` to select.**

## Support
Docs: https://dashboard.alwaysai.co/docs/getting_started/introduction.html

Discord: https://discord.gg/alwaysai

Email: contact@alwaysai.co

