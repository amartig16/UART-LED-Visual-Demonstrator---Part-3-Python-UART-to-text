# UART-LED-Visual-Demonstrator---Part-3-Python-UART-to-text

## ****If this project is useful to you, share your opinions in the comments section****<br> 
## What problem do you have that this project solved?</br></br></br>
### This is the last of a 3 part series:</br></br>
1. uart-led-visual-demostrator-part1</br> 
[https://github.com/amartig16/uart-led-visual-demostrator-part1]</br>
2. UART-LED-Visual-Demonstrator---Part-2-Mobile-Decoder</br>
[https://github.com/amartig16/UART-LED-Visual-Demonstrator---Part-2-Mobile-Decoder]</br>
3. UART-LED-Visual-Demonstrator---Part-3-Values-to-Text</br></br>

#### Quick Start
1.	Record LED blinks using the Flutter capture app
2.	Export brightness values to excel and clean any extra initial values
3.	Paste brightness values as CSV to Python
4.	See the text from an UART value!

#### This Series is Perfect For</br>
* Educators teaching serial communication
* Makers building light-based projects
* Students learning data protocols
* Anyone curious about how information travels</br></br>

#### What does the Python scripts does:</br>
This is a basic script meant to be clearly understood. Thus, its format while reading brightness values and transforming them into text. Letter by letter.</br></br>

* Convert pasted CSV to list</br>
* Converts list into NumPy array for fast processing
* Cluster list into separated lists of X size inside an array, representing higher bright values and low bright values. These late will become 1 and 0.
* Reduce noise in the calculations for clarity when decoding into letters from values
* Transforms brightness values to 1 and 0s [01100101]
* Decodes binary value to text. The above is the letter “e”

#### Recommendations: 
* When recording brightness values, you may have extra values at the start. Remove these values in Excel, so you only have the ones representing the message “Hello World.”
* Only provide brightness values for one letter at a time to the Python script.

#### Observations [these are real-world challenges when processing a light signal]:</br>
Cellphone cameras tend to auto adjust brightness levels.  Therefore, a low value means LED ON, and high value means LED OFF.</br></br>
The brightness values form a digital signal instead of analog one. Thus, the need to divide the frames into high value bright levels and low value bright levels (chunk_size). i.e. App Values: 115,125,127,118,114,106,95,92,80,91,101.  Python: [15,125,127,118,114] [106,95,92,80,91,101]. These will become a binary value [0,1…]. Then, text: “H” </br></br>
Same wise, there is a time delay between the LED turning on and off and the camera registering this change. To compensate for this, reduce speed in the Arduino script from part 1. const int baudRate = 1; (from 5 to 1) this will equal to about one LED pulse per second. Thus, reducing noise in the values and making it easier for your camera to register changes.</br></br>
Keep the phone steady: movements will create noise in the values.</br> </br>     
#### Python Dependencies:  numpy </br></br>
#### How to use the script:
Paste brightens values to the data variable named “data” inside the python script it should look something like this: data = “””123 125 125 96 86…“””  </br> 
#### Go to “Fine tuning controls”:</br>
You can adjust to your taste or leave at default values</br></br>
chunk_size = 10 </br>       Splits the list into an array with smaller lists inside. Each list will have “chunk_size” amount of numbers inside. This is done to separate larger values from the smaller ones for processing later.</br></br>
noise_reducer = 2  </br>     Sometimes large numbers (i.e [130, 125, 80, 80]) gets mixed with the smaller numbers inside a lists. noise_reducer  makes sure to delete the 2 largest numbers inside all lists. Leaving only the smaller values, making it easier later to calculate its average values.</br></br>
delete_list = 1  </br>           In case the array contains more than 10 lists. You can eliminate any extras that contain less than delete_list amount of numbers inside a list. (i.e [125,123,126] … [126]). The list with only one number will be deleted. Leaving 10 lists representing the ten bits in an UART package. Start bit (0) + letter (H) + Stop bit (1) = ten bits in total  

