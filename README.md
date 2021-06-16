# MKEL1123-Milestone5 "Image Classification of Flowers"
# Project Working Procedure
Group members: 
1. Azra Binti Ahmadi MKE201047
2. Low Chun Kang MKE201034
3. Ooi Chee Kean MKE201078

Online Platform and Software involved in this project:
1. Edge Impulse to train the model. <br /> (Sign up for free at https://www.edgeimpulse.com/)
2. STM32CubeIDE to deploy the trained model into microcontroller. <br /> (Download and install from https://www.st.com/en/development-tools/stm32cubeide.html)
3. PuTTY to display test result. <br /> (Download and install from https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)

Build and train model from Edge Impulse:
1. Obtain image dataset from online source. In this project, image dataset used was obtained from https://storage.googleapis.com/download.tensorflow.org/example_images/flower_photos.tgz.
2. Upload training and test data to Edge Impulse through the uploader. Click 'LET'S COLLECT SOME DATA' and choose 'Go to the uploader'. <br /> ![image](https://user-images.githubusercontent.com/82256749/122092767-e3320d80-ce3c-11eb-94c5-dbc22e5182b2.png)![image](https://user-images.githubusercontent.com/82256749/122093204-65bacd00-ce3d-11eb-859f-9ad8263e2e23.png)
3. In Data acquisition, choose the images of same class that need to be uploaded. Select 'Training' category for training data while 'Testing' catogerry for test data. Choose 'Enter Label' to label the image class. Finally, click 'Begin Upload'. Repeat this step with other image classes. <br /> ![image](https://user-images.githubusercontent.com/82256749/122094420-c0a0f400-ce3e-11eb-8ad3-0256e82e9db2.png)
4. After all images are uplaoded, start to create impulse. Set both image width and height to be 32 and resize mode to 'Fit shortest axis'. Add a 'Image' processing block to process the image and generate features and a 'Neural Network (Keras)' learning block for the data training. <br /> ![image](https://user-images.githubusercontent.com/82256749/122095557-1fb33880-ce40-11eb-910c-6296d7c245ef.png)
5. Go to Image section, choose the colour depth as 'RGB' and save the parameters. Then, click 'Generate features' and wait till the process is done. <br /> ![image](https://user-images.githubusercontent.com/82256749/122096079-ba137c00-ce40-11eb-9cea-7cec16bdb055.png)![image](https://user-images.githubusercontent.com/82256749/122096118-c8fa2e80-ce40-11eb-99bc-16defa6eebfb.png)
6. Start to train image in NN Classifier section. Set 100 training cycles, 0.0005 learning rate and 0.60 minimum confidence rating and click 'Start training'. Wait till the training process is done and check the accuracy of the training performance. <br /> ![image](https://user-images.githubusercontent.com/82256749/122097207-feebe280-ce41-11eb-945b-fbc61c151f26.png)
7. If the training perfomance is satisfied, go to Model testing section to test the accuracy of the trained model on test data. Click 'Classify all' to start the process and check the validation results after the job is completed. <br /> ![image](https://user-images.githubusercontent.com/82256749/122097738-97826280-ce42-11eb-91e7-a145617eaa34.png)
8. Deploy the impulse after the model is successfully trained. In Deployment section, choose 'Cube.MX CMSIS-PACK', and select 'Quantized (int8)' optimization. Finally, click 'Build' to download the output pack file. <br />  ![image](https://user-images.githubusercontent.com/82256749/122098528-8be36b80-ce43-11eb-96e1-7d21101d7eb5.png)![image](https://user-images.githubusercontent.com/82256749/122098578-9c93e180-ce43-11eb-8dfa-7700be397e5e.png)

Deployed trained model into microcontroller by STM32CubeIDE:
1. Start a new STM32 project in STM32Cube IDE software.
2. Under Board Selector tab, find the model code of the microcontroller and click 'Next'. In this project, we used Nucleo-F446RE microntroller.
3. Enter the project name and select 'C++' as targeted language. Then, click 'Finish'. If there is a pop up, click 'Yes' to initialize all peripherals with their default Mode.
4. Open .ioc file, go to 'Pinout & Configuration' > 'Computing' > 'CRC' to enable 'Activavated' checkbox. <br /> ![image](https://user-images.githubusercontent.com/82256749/122222573-fac4d100-cee4-11eb-8921-61ecb2e7e7d3.png)
5. Then, add in the pack downloaded from Edge Impulse to the project. Go to 'Help' > 'Manage Embedded Software Packages' > 'From Local...' and select the downloaded pack. Accept the license agreement and thepack will be installed. <br /> ![image](https://user-images.githubusercontent.com/82256749/122222796-2d6ec980-cee5-11eb-9284-5b426ed17b4a.png)
6. After installing the pack, go back to .ioc file. This time goes to 'Pinout & Configuration' > 'Software packs' > 'Select components'. Select your project, expand the pack, and click a checkbox under 'Selection'. Then click 'OK' to close the window. <br /> ![image](https://user-images.githubusercontent.com/82256749/122224923-2943ab80-cee7-11eb-99d9-cac74449dfc7.png)
7. Go back to 'Pinout & Configuration', under 'Additional software', click on the project name. enable a checkbox next under 'Mode'. <br /> ![image](https://user-images.githubusercontent.com/82256749/122226915-fbf7fd00-cee8-11eb-9187-f22ca28ba461.png)
8. Click in the 'Project explorer' so the .ioc file loses focus. Press CTRL+S to save the workspace. This will regenerate the code and afterward, a 'Middleware' folder can be seen in the project explorer with your impulse and all required libraries. Rename the "main.c" file under Core/Src in "Project Explorer" to "main.cpp", as C++ language is preferred to be used. <br /> ![image](https://user-images.githubusercontent.com/82256749/122232464-d6212700-ceed-11eb-82e1-6e0d7f801c82.png)
9. Edit the main.cpp script or copy from here. (https://github.com/LowChunKang/MKEL1123-Milestone5/blob/main/Core/Src/main.cpp)
10. Click the 'Hammer' icon to build and compile the project. Then, connect the microcontroller and click 'Play' to start deployment. Leave all settings as default and click'OK'. (Message below shows the deployment is succeed) <br /> ![image](https://user-images.githubusercontent.com/82256749/122233989-0e753500-ceef-11eb-93c2-59cf0a00a4c5.png)

Connect PuTTY to display output of microcontroller:
1. Open 'Device Manager' to check which USB COM is connected. <br /> ![image](https://user-images.githubusercontent.com/82256749/122234459-76c41680-ceef-11eb-87e1-acd8b136fee2.png)
2. Open PuTTY, change the connection type to 'Serial', enter the USB COM in 'serial line' column and set the speed to 115200. Then, click 'Open'. <br /> ![image](https://user-images.githubusercontent.com/82256749/122234890-d15d7280-ceef-11eb-8b3a-18b1b22147ad.png)
3. Finally, the output can be seen from PuTTY serial console. The results can be compared with test result from Edge Impulse. <br /> ![image](https://user-images.githubusercontent.com/82256749/122235462-4c268d80-cef0-11eb-8102-bc5695875ae4.png) ![image](https://user-images.githubusercontent.com/82256749/122235557-5f395d80-cef0-11eb-8921-59de1f7b8a54.png) <br /> 
(This section of the code can be filled in with any raw features of image classes obtained from Live Classification section in Edge Impulse to be tested.) <br /> ![image](https://user-images.githubusercontent.com/82256749/122235596-67919880-cef0-11eb-9bed-2ea393f507c2.png) ![image](https://user-images.githubusercontent.com/82256749/122235639-6fe9d380-cef0-11eb-8c4c-ba9c760f4076.png)
