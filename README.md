# Overview:
-  The question use a method of hiding data which involves hiding that part of an image which displays necessary infomation.
Every file has a specific sturcture and changing this structure leads to different properties of the file being shown or hidden. For 
an image file, the binary of this file contains information such as the file type, dimension of the image, color schema etc. For this
question we go to the part which stores the dimensions of the visible part of the image. To do this we look at the hex of the file. 
Our required part starts after the code ***ff c0***. A look into the website:
              https://cyberhacktics.com/hiding-information-by-changing-an-images-height/
gives further information about this type of encryption. Now we change the part which stores information about the height of the
image and hide out information. This can later be undone to retrive the image. the question also involve the use of Base64 encryption.

***

# Procedure:
-  The question contains a compressed file which, upon extraction, gives us an ***.jpg* file named *cover.jpg* . At first glance, the problem
looks like something related to steganogrphy, and it in fact is. Since it is a *.jpg* file, we proceed further by using *Steghide*. 
Steghide is a tool used to hide files in *bmp, jpp, jpeg and au* files. But using steghide also requires a passphrase. We find the 
passphrase by looking at the hex of *cover.jpg*. This can be done by opening the file in any hexeditor or in the terminal itself by 
using the command ***hexedit cover.jpg***. At the end of the hex, we find the string ***"The password is obvious"***. We type the password in
the field provided after typing the command ***"steghide extractn -sf cover.jpg"***. Steghide extracts a file named *download.jpg* from cover
.jpg . If one does the preliminary analysis on this file , be it looking at it's hex or using the file command on it or inspecting it
using binwalk, nothing seems suspicious. But when we resize the image by changing it's hex, we see a text visible at the bottom part
of the image. We note the text, which at first glance itself looks like a *Base64* encryption due to the '='s in the end. We can use an 
online decryption tool like *cryptii* to decrypt the code and obtain the flag.(Also remember to remove the three '=' signs in the end 
since the length of the encrytion is already a multiple of 3).
 
