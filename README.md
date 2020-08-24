# Age-prediction

The convolutional neural networks (CNNs) use the VGG-16 architecture and are pretrained on ImageNet for image classification.
The model estimates age from a single face image without the use of facial landmarks. The model has been pretrained on the IMDB-WIKI dataset the largest public dataset of face images with age and gender labels. The pretrained weights can be found [here](https://drive.google.com/file/d/1mLaHLJR67kHFRSEdn8LN8rsIIZ-9HiDk/view?usp=sharing)

## Usage
There is a .mat file for Wikipedia images which can be loaded with Matlab containing all the meta information. I will be using the cropped images for the sake of memory.Download the tar file from [here](https://drive.google.com/file/d/1c-J7_fTziGxqy54AZUEAnyx6wSAxii-w/view?usp=sharing) and untar in the working directory.

The format is as follows:

dob: date of birth (Matlab serial date number)

photo_taken: year when the photo was taken

full_path: path to file

gender: 0 for female and 1 for male, NaN if unknown

name: name of the celebrity

face_location: location of the face. To crop the face in Matlab run

img(face_location(2):face_location(4),face_location(1):face_location(3),:))

face_score: detector score (the higher the better). Inf implies that no face was found in the image and the face_location then just returns the entire image.

second_face_score: detector score of the face with the second highest score. This is useful to ignore images with more than one face. second_face_score is NaN if no second face was detected.

celeb_names (IMDB only): list of all celebrity names
celeb_id (IMDB only): index of celebrity name

The age of a person can be calculated based on the date of birth and the time when the photo was taken (note that we assume that the photo was taken in the middle of the year):

[age,~]=datevec(datenum(wiki.photo_taken,7,1)-wiki.dob); 


@article{Rothe-IJCV-2018,
  author = {Rasmus Rothe and Radu Timofte and Luc Van Gool},
  title = {Deep expectation of real and apparent age from a single image without facial landmarks},
  journal = {International Journal of Computer Vision},
  volume={126},
  number={2-4},
  pages={144--157},
  year={2018},
  publisher={Springer}
}
