# Identifying People With Glasses
This project identifies whether or not someone is wearing glasses. In many situations where authorities are trying to find someone with specific features, it would be useful to be able to easily identify whether or not people in surveillance footage have glasses.
## The Algorithm
This project takes a Resnet 18 network that has been pretrained with  a large dataset to classify more than 1000 objects. It will retrain this network to identify new classes, or in my case, people with glasses and people without glasses. To do this, I downloaded a dataset containing images of people with and without glasses and used it to retrain the network. At the end of the training, the new model is able to identify whether or not a person is wearing glasses.
## Running this Project
1. First download the necessary dataset by visiting the Kaggle webpage: https://www.kaggle.com/datasets/jorgebuenoperez/datacleaningglassesnoglasses. Click the “download” button to download the dataset. After downloading, unzip the dataset. This will put the images into two folders: “glasses” and “no_glasses.” 
2. Now create 3 folders titled “test,” “train,” and “val.” Move about 80% of the images into the “train” folder, ensuring they are separated into “glasses” and “no_glasses” folders. Split the remaining images into the “test” and “val” folders following the same process. Add images you want to test into the “test” folder (in jpg form). 
3. Move these files into the jetson-inference/python/training/classification/data folder in jetson nano. 
4. In a terminal, in the jetson-inference directory, run the docker by running “./docker/run.sh”
5. Change directories into jetson-inference/python/training/classification. Then run “python3 train.py --model-dir=models/glassvsnoglasses” to train the network.
6. To convert the model to ONNX format, run “python3 onnx_export.py --model-dir=models/glassvsnoglasses”
7. Press ctrl+D in the docker terminal to exit docker. Confirm your directory is in jetson-inference/python/training/classification. Then set the locations of net and dataset by running “NET=models/glassvsnoglasses” and “DATASET=data/glasses_no_glasses” 
8. To classify an image as wearing glasses or not wearing glasses, type: imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/glasses/[image name].jpg result.jpg. Type the name of the image you want to test in the square brackets and delete the square brackets.

View a video demonstration here: https://youtu.be/lIGNOew6NyM
