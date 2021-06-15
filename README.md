# MKEL1123-Milestone5 "Image Classification of Flowers"
# Project Working Procedure
Group members: 
1. Azra Binti Ahmadi MKE201047
2. Low Chun Kang MKE201034
3. Ooi Chee Kean MKE201078

Online Platform and Software involved in this project:
1. Edge Impulse to train the model. <br /> (Sign up for free at https://www.edgeimpulse.com/)
2. STM32CudeIDE to deploy the trained model into microcontroller <br /> (Download and install from https://www.st.com/en/development-tools/stm32cubeide.html)
3. PuTTY to display test result <br /> (Download and install from https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)

Build and train model from Edge Impulse:
1. Obtain image dataset from online source. In this project, image dataset used was obtained from https://storage.googleapis.com/download.tensorflow.org/example_images/flower_photos.tgz.
2. Upload training and test data to Edge Impulse through the uploader. Click 'LET'S COLLECT SOME DATA' and choose 'Go to the uploader'. <br /> ![image](https://user-images.githubusercontent.com/82256749/122092767-e3320d80-ce3c-11eb-94c5-dbc22e5182b2.png)![image](https://user-images.githubusercontent.com/82256749/122093204-65bacd00-ce3d-11eb-859f-9ad8263e2e23.png)
3. In Data acquisition, choose the images of same class that need to be uploaded. Select 'Training' category for training data while 'Testing' catogerry for test data. Choose 'Enter Label' to label the image class. Finally, click 'Begin Upload'. Repeat this step with other image classes. <br /> ![image](https://user-images.githubusercontent.com/82256749/122094420-c0a0f400-ce3e-11eb-8ad3-0256e82e9db2.png)
4. After all images are uplaoded, start to create impulse. Set both image width and height to be 32 and resize mode to 'Fit shortest axis'. Add a 'Image' processing block to process the image and generate features and a 'Neural Network (Keras)' learning block for the data training. <br /> ![image](https://user-images.githubusercontent.com/82256749/122095557-1fb33880-ce40-11eb-910c-6296d7c245ef.png)
5. Go to Image section, choose the colour depth as 'RGB' and save the parameters. Then, click 'Generate features' and wait till the process is done. <br /> ![image](https://user-images.githubusercontent.com/82256749/122096079-ba137c00-ce40-11eb-9cea-7cec16bdb055.png)![image](https://user-images.githubusercontent.com/82256749/122096118-c8fa2e80-ce40-11eb-99bc-16defa6eebfb.png)
6. Start to train image in NN Classifier section. Set 100 training cycles, 0.0005 learning rate and 0.60 minimum confidence rating and click 'Start training'. Wait till the training process is done and check the accuracy of the training performance. <br /> ![image](https://user-images.githubusercontent.com/82256749/122097207-feebe280-ce41-11eb-945b-fbc61c151f26.png)
7. If the training perfomance is satisfied, go to Model testing section to test the accuracy of the trained model on test data. Click 'Classify all' to start the process and check the validation results after the job is completed. <br /> ![image](https://user-images.githubusercontent.com/82256749/122097738-97826280-ce42-11eb-91e7-a145617eaa34.png)
8. Deploy the impulse after the model is successfully trained. In Deployment section, choose 'Cube.MX CMSIS-PACK', and select 'Quantized (int8)' optimization. Finally, click 'Build' to download the output pack file. <br />  ![image](https://user-images.githubusercontent.com/82256749/122098528-8be36b80-ce43-11eb-96e1-7d21101d7eb5.png)![image](https://user-images.githubusercontent.com/82256749/122098578-9c93e180-ce43-11eb-8dfa-7700be397e5e.png)
