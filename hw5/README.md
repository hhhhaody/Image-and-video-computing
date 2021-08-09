

    

    <hr>
    <h2> Description</h2>
    <p>
    The project requires us to use OpenCV to create a program which tracks ojects from input video. We use Kalman Filter Algorithm to correct our frame-to-frame 
    measurements and bipartite matching to up the predictions produced by Kalman Filter and the actual measurement. 
    
    </p>
    
    <hr>
    <h2> Method and Implementation </h2>
    <p>
    In order to get the contours from the image, we use code from previous lab 7. We get the first image from the video, and then we change the image
    to gray scale so that we can contain a binary verison of the image. In the function threshold given in lab7, we modify the parameter to fit the specific dataset.
    We get a list of contours from findContours in function threshold, and since not all detected contours are the wanted objects, we then perform a function called area
    with contours and a int as inputs. This function helpes us to remove all the contours that were smaller than the set variable so that some small objects could be 
    removed from the window.  
      
    <br> <br>
    
    A class track is created to hold the color, position, movement history, and its kalman filter while we moving forward to the next image. With the contours from the first frame , we use function area to gather all the objects that needed to be tracked. We created a track object for each contour in the contour list for the first image. As the 
    while loop proceeded, we compute the prediction for each track object and compared this prediction with the measurements from the second frame. 
    
    <br> <br>
    
    A bipartite matching is used to find the matching pair. We first calculate the pairwise distance between object centers from the previous frame and the current frame as the cost matrix, and use the function linear_sum_assignemnt to do the matching. It returns 2 index list. From the lists, we can know the unmatched points and differenciate them through some set parameters. If the point matched with existed point, we check if the distance between matching points from two frames are too large that they seem not to be the same one. If the matching is reasonale, we update the poition and track history in the specific track object. 
    If it was unmatched, we create a new track object and add the object at the end of the track list. Based on the track list, we draw the track history and the bounding 
    box for each track. 
    
    
    </p>
    
    
    <hr>
    <h2> Results</h2>
    <p>
    <dt></dt>
    <video width="480" height="512" controls>
        <source src="bat.mp4" type=video/mp4>
      </video>
    
    <video width="480" height="512" controls>
      <source src="cell.mp4" type=video/mp4>
    </video>
    
    </p>
    
    
    <hr>
    <h2> Discussion </h2>
    
    <p> 
    From the bat video, most bats can be identified successfully. One of the challenge situation is when two bats encountered each other,
    and our code can handle this situation relatively smoothly. However, one of the problem we had was tracking the bats that were far 
    away from the camera. Since the contours for them were small, which can be also removed when we removed the stars. Because our code 
    was based on the contours and the area of bounding box to determine which contours were objects that needed tracking, we might lost 
    the track of some bats that only can be detected discretely. 
    <br><br>

    When deciding whether to begin new tracks and terminate old tracks as the objects enter and leave the field of view,
    If it was the first frame of the video, we would create a track object to the track list for all detected contours which had certain 
    amount of area. If the program was in the frame other than the first frame, we would compare the predicted positions based on the existed 
    track objects with the current measurments. The prediction is done by Kalman Filter, and the matching is done by bipartite matching. 
    From the returned index lists, if some existed track object did not match with a current measurement, we would define it as lost and its 
    position and track history would not be updated. If some cureent measurement did not match with any existed track object, we define it as 
    new object. We create a new track object and add it to the end of the track list. 
    

    <br><br>

    In our case, when two objects occlude with each other, the prodiction from Kalmen Filter algorithm helps us to identify which measurement 
    belongs to which track object. Spurious detections would not affect our tracking because if a detection appeared and unconnected with other 
    measurements, then it would define as new object becuase it was distant from other objects. Since we draw the track history based on the 
    cv2 function line, the track history of this object would never be shown in the video with only one point in its tracking history.  

    <br><br>

    One adventage for Kalman Filter is that we only need to set our matrices, and the embedded Kalman Filter does rest of the work for us. We did 
    not model the velocity. Rather, we model noise in our Kalam Filter and only consider distances between objects. Our method reqiures many parameters 
    that need to be set manually. 
    
    </p>
    
    <hr>
    <h2> Conclusions </h2>
    
    <p>
    In conclusion, our program can successfully detect different objects and track his movement with the help of Kalman Filter and bipartite matching.
    The result is relatively smooth without considering the velocity of objects.   
    </p>
    
    
    <hr>
    <h2> Credits and Bibliography </h2>
    <p>
    https://docs.opencv.org/master/dd/d6a/classcv_1_1KalmanFilter.html
    https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.linear_sum_assignment.html
    </p>
    
    <hr>
    </div>
    </body>
    
    
    
    </html>
    
