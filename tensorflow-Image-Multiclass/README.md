#Up and running the code for Tensorflow

1/ Download the image directory from
curl -O http://download.tensorflow.org/example_images/flower_photos.tgz

tar xzf flower_photos.tgz

2/ docker run -it  gcr.io/tensorflow/tensorflow:latest-devel

3/ $ docker run -it -v $HOME/tf_files:/tf_files gcr.io/tensorflow/tensorflow:latest-devel

4/ Inside the container ,do (to get the latest tensorflow code)
cd /tensorflow
git pull

5/ Run this on the commandline (Should take around 30-45 min for the training)
python tensorflow/examples/image_retraining/retrain.py \
--bottleneck_dir=/tf_files/bottlenecks \
--how_many_training_steps 4000 \
--model_dir=/tf_files/inception \
--output_graph=/tf_files/retrained_graph.pb \
--output_labels=/tf_files/retrained_labels.txt \
--image_dir /tf_files/flower_photos

6/ To bypass copy-pasting the prediction code (Dowload from the URL)
# ctrl-D to exit Docker and then:
#Inside Host Machine
% curl -L https://goo.gl/tx3dqg > $HOME/tf_files/label_image.py

7/ Restart Docker image:
% sudo docker run -it -v $HOME/tf_files:/tf_files  gcr.io/tensorflow/tensorflow:latest-devel

8/ Predict/Test :

python /tf_files/label_image.py /tf_files/flower_photos/daisy/21652746_cc379e0eea_m.jpg



Below are the sample predictions for daisy, roses respectively :

$ python /tf_files/label_image.py /tf_files/flower_photos/daisy/21652746_cc379e0eea_m.jpg

daisy (score = 0.99772)
sunflowers (score = 0.00143)
dandelion (score = 0.00059)
tulips (score = 0.00015)
roses (score = 0.00011)

$ python /tf_files/label_image.py /tf_files/flower_photos/roses/2414954629_3708a1a04d.jpg

roses (score = 0.98141)
tulips (score = 0.01783)
dandelion (score = 0.00037)
sunflowers (score = 0.00033)
daisy (score = 0.00006)










