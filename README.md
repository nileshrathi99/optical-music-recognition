OPTICAL MUSIC RECOGNITION

The program utilizes advanced image processing techniques to extract musical notes hidden within an image. Before running the code, it is necessary to ensure that all the required libraries and dependencies are installed, such as Pillow, NumPy and Numba (for faster execution). Once installed, the code can be executed and the image containing musical notes can be uploaded for analysis.

The program's note extraction process involves identifying the treble and bass clefs using the Hough transform feature detection technique. The program assumes that the lines representing the clefs are horizontally positioned at 0 degrees. The program calculates the number of white and black pixels for each row in the image and considers a row a line if it has more black pixels than white. It checks for any rows that are too far apart and sorts them by position in the image, locating the first position on the treble clef. The program ensures that the first position on the bass clef is located on a row that is at least 50 units away from the previous row. This process continues until all the positions for the treble and bass clefs are located. The program also calculates the distance between the lines to know at what height to reshape the template image.

To locate the treble and bass clefs, we assumed that the lines were horizontally positioned at 0 degrees. We then calculated the number of white and black pixels for each row in the image and determined that a row could be considered a line if it had more black pixels than white. We checked for any rows that were too far apart, as no two lines could be more than 8 units away from each other. Once we had all the potential lines, we sorted them by position in the image and located our first position on the treble clef. We then made sure that the first position on the bass clef was located on a row that had more than 50 units distance from the previous row. We continued this process, locating the treble clef and bass clef positions alternately. Moreover we also calculated the distance between the lines, so that we could know at what height we need to reshape our template image. The distance was taken as a mean of the difference between the first four lines of treble.

The initial step involved identifying the clefs and exploring the grayscale features of the musical image and the template image containing notes. To ensure accurate matching, we adjusted the height of the template image to correspond with the distance between the staff lines. In the subsequent stage, we computed the intersection over union between the template kernel and the musical image for template matching. To achieve this, we converted both images to binary and picked potential locations based on a threshold that was adjusted through experimentation to obtain all possible locations. Although this method was fast, it did not capture all the desired possibilities.  An alternative approach involved cross-correlation, which was applied to match the template notes with the music image, and it was observed that pixel normalization was crucial to obtain accurate locations of the notes. The resulting cross-correlation score represented the degree of similarity between the template and the music image at each position. Through experimentation, a threshold was determined for each template to identify potential note locations in the score map. This approach produced multiple bounding boxes that had overlapping regions. To resolve the redundancy issue, the non-max suppression algorithm was employed where if more than 1 boxes have an overlap of 5% only one is considered and rest were discarded, which retained only the most probable location for each note by eliminating the overlapping boxes. The threshold value for eliminating the redundant boxes was determined by experimentation.

Before non-max suppression:

![image](https://github.com/nileshrathi99/OMR/assets/32071800/e6973249-1290-4600-90fe-e596d18756e0)


After non-max suppression:

![image](https://github.com/nileshrathi99/OMR/assets/32071800/f93952ec-4e52-416d-a5f0-d0eec367f243)




The program extracted notes from the image by determining the pitch of each note based on its corresponding clef. This was achieved by establishing the minimum distance between the note's position and the clef's position. Once the clef was established, a predefined dictionary was referenced to determine the note's pitch based on the units it was away from the clef. The pitch and location details of the notes were then displayed using a font downloaded from Google (https://fonts.google.com/specimen/Roboto), which created visually captivating results. 

The program was able to extract notes accurately when they were clearly defined in the image and the template matched the music genre. However, it failed to detect the pitch correctly when the notes were too small or too close together. 

To improve the program, machine learning algorithms could be implemented to train the model on various music genres, which would allow for more accurate note extraction. Additionally, the pitch detection algorithm could be enhanced to handle more complex note arrangements, such as identifying and removing connecting components that should not be considered as a possible location of a note.

 

In the future, our program could be improved by implementing machine learning algorithms to train the model on various music genres, allowing for more accurate note extraction. We could also work on improving the pitch detection algorithm to handle more complex note arrangements. Such as we can detect the connecting components and remove it from being considered as a possible location of a note, Despite its limitations, we believe our program is a unique approach to extracting musical notes from images.


![music1](https://github.com/nileshrathi99/OMR/assets/32071800/7ab1a754-102f-4893-b25e-b7ce77d77ed3)


![detected](https://github.com/nileshrathi99/OMR/assets/32071800/e9c3bc4d-73e3-490f-840a-c3a981411041)



