## Final Project for COMS 3101 - Web App for People Detection
## Tomer Solomon Mate, ts2838

IMPORTANT: Please run with Python 2.7, as OpenCV does not support Python 3 and is the main library I used for the computer vision. 

### Description

For my final project, I decided it would be fun to create a basic web app in Flask that uses machine learning to detect people in videos (MP4 format) and images (JPEG format). I am interested in all the current hype around autonomous driving, such as the work companies like Tesla as well as car companies like Ford are doing in helping spur the next generation of autonomous vehicles, and thought this would be a cool project to get my hands dirty with how exactly this autonomous driving works at an elementary (read: very elementary) level. Computer vision in general interests me and is all around us as well, from Facebook facial recognition to Google generating tags for the photos we upload to Google Photos (almost scary how well Google photos searches through your photos).

As such, I thought it would be cool to implement a basic people detection algorithm as a final project for this class. I experimented around with Flask as well to dabble in how basic web application works. I used OpenCV as the main library for computer vision work as it is the leading and one of the most powerful computer vision libraries, and wanted to get experience with how it worked. Becasue it was first coded up in C/C++ then transferred over to Python however, the documentation wasn't necessarily the best. Specifically, the machine learning algorithm is a support vector machine pretrained on the INRIA Person datasets. 

Below are a couple examples of analyzed images:

![alt text](https://github.com/tomersolomon/TheEye/blob/master/analyzed_examples/Screen%20Shot%202016-11-16%20at%2011.19.11%20PM.png "Logo Title Text 1")

![alt text](https://github.com/tomersolomon/TheEye/blob/master/analyzed_examples/Screen%20Shot%202016-11-16%20at%2011.19.23%20PM.png "Logo Title Text 1")


A video demo is saved down as "video_demo.mp4" in the folder, which is a screen cast of the app in action!




### Code Structure

Part 1, the machine learning part, is made up of three functions. The first function, detect_human, reads in an image using matplotlib's imread, then creates a HOG features space, then detects people, then draws a green box around detected people, and finally saves the file in the project_directory + '/static/results/' folder. The HOG feature space is an abbreviation for Histogram of Oriented Gradients, and is one of many feature spaces used in machine learning that reduces the dimensions of the image by some mathematics I'm not 100% familiar with. The video_detect_human algorithm is pretty much the exact same except the input is an array rather than a string. The final function is the save_video function, which was a little trickier. I used OpenCV's VideoCapture to read in a video, where fourcc corresponds to the type of compression and VideoWriter object saves the created movie. It then iterates over every frame, applies the vide_detect_human function, saves each frame, and then releases everything when done. A point to note is that it takes a while to create the video (about 20 seconds for 2-3 seconds). Part 2 is made up of the Flask application. The first part of the app is the creation of the index.html page, which basically takes an movie/image and uploads it to the /static/uploads folder.  If the file is an image, it redirects to the image html page, and if the file is a movie, it redirects to the video html page.

### How to Run

The app is  run locally on http://localhost:5000/. In order to run it, you simply run the code below after changing the project_directory variable to the directory where the Project folder is saved. You then upload images/videos to the app, and I put sample images and videos in the respective sample_images and sample_videos folder of the Project folder for you to play around with. Don't change around the order of any of the files within the Project folder, since the current structure allows images/videos to be saved in the uploads and results folder as well as for the Flask app to perform the render_template function properly. The ipython notebook should also not be moved around. Certain packages need to be installed, which I will cover below. 


### Dependenices

As far as dependenices go, the trickest package to install is OpenCV. I spent a while figuring out how to do this, as one can't simply pip install OpenCV. To do so, You "conda install -c https://conda.binstar.org/menpo opencv" in the terminal. Make sure that the python version you are using is Anaconda. When I run "python -V" in terminal, I get Python 2.7.12 :: Anaconda 4.1.1 (x86_64).

You need to also install imutils (simply pip install imutils), which is used for image processing. Other libraries that are used, which can be seen below, are: os, flask, werkzeug, numpy, and matplotlib. All these have straightforward pip installs.


### Problems Encountered

There were definitely a good amount of road blocks along the way. For the ML algorithm part, fortunately I didn't have to build any algorithm from scratch as it came nicely packaged in OpenCV, but I still had to figure out how exactly  HOG.Descripter and setSVMDetector worked. I also had problems initially with figuring out how to save an MP4, as the ImageCapture documentation was obscure. The saving of the video took a while since the VideoCapture and VideoWriter class don't have great documentation, and I had to guess around with the the type of fourCC code to use since initially when I was using MP4, the video wouldn't play in the HTML for some unknown reason.  I had hiccups figuring out how to get the filename variable to pass through to the other app routes, but eventually figured it out. I also took some time trying to figure out how to display variable names in the HTML, which is more of a Jinja syntax problem then a pure python one. The last part of the flask app simply runs the app.


### Python Evaluation

Overall, I thought Python and Anaconda in particular was a good platform to create this project, particularly the machine learning component of the project. Python is particularly good because you are able to import libraries like OpenCV which allow people to get the ball rolling much quicker, rather than having people create entire classes by themself. I also found Matplotlib helpful in creating pictures of the images and visualizing the people detection, and thought that Python has a good system for saving down files locally (like how I saved down files into the uploads folder and results folder). I wonder how effective Python would be when it comes to interacting with servers. I know there was a brief PDF on SQL and Python in the Coursworks, but I didn't see any information on storing images/videos in a SQL database. While I found Flask to be a good starting point for web application and good for this purpose, I wonder how effective it would be for larger apps and how it would scale, so I don't believe I Python would be as good for web application necessarily. I looked into it, and there are other web frameworks like Django which might be more effective for bigger web applications. 

### Final Thoughts

Overall, I had fun making this little app. In the future I want to work with how I can effectively store images in a database rather than just save them down locally, and I want to also learn how deployment works on applications like Heroku. Also room for improvement is speeding up the analysis of movies, which now takes a while. 

Please email me know if you have any questions/any problems when running it at ts2838@columbia.edu. Hope you enjoy!
