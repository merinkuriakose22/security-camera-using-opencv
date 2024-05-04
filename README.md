# security camera using opencv
  How to capture webcam and using opencv and python. Finding the difference between the captured images using cv2 function. Then using winsound to make sound when the webcam captures an object in the screen.  The opencv-python library and winsound library are imported in the code and the cv2.VideoCapture(0) method is used to capture the video from the web cam and webcam.read() method converts the captured to an image object and stores in a variable.  Open cv method cv2.absdiff(image1,image2) is used to find the difference between two captured objects. Then the difference is converted to gray scale image. Then the cv2.threshold(gray,20,255,cv2.THRESH_BINARY) method converts the binary image.   Then making contours using cv2.findContours(thresh,cv2.RETR_TREE,cv2.CHAIN_APPROX_SIMPLE) and find the areas.  If any object found then this opencv project will make a sound using winsound.Beep(500,100) method.
  import cv2
import winsound
webcam = cv2.VideoCapture(0)
while True:
    _,im1 = webcam.read()
    _,im2 = webcam.read()
    diff = cv2.absdiff(im1,im2)
    gray = cv2.cvtColor(diff, cv2.COLOR_BGR2GRAY)
    _,thresh = cv2.threshold(gray,20,255,cv2.THRESH_BINARY)
    contours,_ =cv2.findContours(thresh,cv2.RETR_TREE,cv2.CHAIN_APPROX_SIMPLE)
    for c in contours:
        if cv2.contourArea(c) < 5000 :
            continue 
        winsound.Beep(500,100)
    cv2.imshow("security camera",thresh)
    Key =cv2.waitKey(10)
    if Key == 27:
         break
webcam.release()
cv2.destroyAllWindows()


