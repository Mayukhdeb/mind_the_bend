# mind_the_bend :racing_car:
Vision based deep learning for racing games. 

![3 channel 56*80 RGB image](https://github.com/Mayukhdeb/mind_the_bend/blob/master/images/pipeline.png "3 channel 56*80 RGB image being fed into the CNN which returns steering values")
>Currently trying to make it work on an open source racing game Speed Dreams - http://www.speed-dreams.org/
>But will work on other racing games as well

## :movie_camera:	Collection of training data -
* Rapidly takes screenshots of the game and saves them in a folder
* The label in this case is the x-co-ordinate of the mouse which is captured by pyautogui and is stored in the formatted filename of each collected image
> image fileame formatting is done as  (x-value)_(unique_ID).png

##  :mag_right: Processing images
* Converts all images to 56*80 numpy arrays with a depth of 3 for R.G and B color channels 
* The shape gets changed from  ``` [ width, height, depth ] ``` to ```[ depth, width, height]``` for it to be of the right size for the CNN input channel
* Pairs them with the corresponding mouse x-coordinate as array [  [[[image]]]  ,  [x-value]   ]
* all of the generated pairs are then stacked into one numpy array with the help of np.vstack() and saved 

## :chart_with_upwards_trend: Data preprocessing and augmentation
* First things first, plotted the frequency distribution of each steering value hen
* Roughly doubled the amount of training data by generating mirror images of existing images and vstacking them with reversed steer value. 
*  Flattened the frequency distribution by making copies of random ramples of under-represented steering value data points
* Normalised the steering values by replacing the x-co-ordinates with steering values. In my case the "straight" steer value was at x = 400, for normalised_value = 400 - x_value. 
> note :  Right is negative steer value and left is positive

## :red_car: Self driving 
* Rapidly taken screenshots are prerpocessed and fed to the trained CNN drunk_driver()
* drunk_driver() returns a steer value 
* Returned value is taken care  of by pyauogui which moves the mouse accordingly 

### Stuff that's under way right now - 
* take screenshots at a higher framerate both while collecting training data and testing trained models 
* Figuring out a better data augmentation technique, instead of just making copies 

## :heavy_exclamation_mark: need help
* need a proper way to terminate/pause the loop in wear_your_seatbelts.ipynb when the CNN takes over mouse control
* ~~kernel dies after about 5 mins of data collection in collect_training_data.ipynb~~
