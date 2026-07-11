---
title: Sending images about a real LG machine.
contributor: Gerard Monsó
date: June 10, 2024
---
## Overview
\
***Introduction***\
\
Each entry has to have the clearest definition of what the entry is, and what part of the Liquid Galaxy handles, it can be UX side (functions on the apps in Flutter or JAVA) or the rig side (all the things related to the Liquid Galaxy cluster and his network, including the AI server and the Dockers we use).\
Please write with clarity for others to understand, and quote code in the right way.
Add graphics if needed, and remember to store the images in the same folder independently.\
TIP: it's better that you send us a previous email with what 3 contents you want to create for the wiki, as many other contributors may have chosen the same.\
Each entry has to be a minimum of half a page, as you have to explain the aforementioned parts and the code or instructions involved.\
You’ll be credited if the entry is published, and also you can be invited to write other ones if the ones you choose have been already written many times.\
Send proof of this task to liquidgalaxylab@gmail.com with the link of the shared Google Drive folder, with open-to-anybody link permissions as mentors will need access to it. Have this folder ready for all the processes.\
Please name the doc with your name and GSoC2024.  We’ll not accept pdfs or .docx
Drop too a DM to admins in our Discord saying the doc is ready.\
\
→ Migration from pub.dev ssh to dartssh2 with version 3.x of flutter\
→ key points for installing the LG that generate the most common errors.\
→ Sending images about a real LG machine.\
\
``` ```
***
\
***Snippet 1: Sending Data to Liquid Galaxy***
```terminal
_lgService.sendKml(
   satelliteData.toPlacemarkEntity(),
   images: [
 {
   'name': 'fire.png',
   'path': 'assets/images/fire.png',
 }
]
);
```
\
1 -  This snippet uses a service called _lgService to send data in KML format. KML is a language for expressing geographic information and annotations, commonly used in visualization tools.\
2 - The data that is sent includes two parts:\
\
2.1 -  Placemark Entity: Created from satelliteData using toPlacemarkEntity(). Represents a specific location or point of interest on the map.\
\
2.2 - Images: The code provides a list of images with their names ('name') and paths ('path') within the app's assets.\
\
``` ```
***
\
***Snippet 2: Uploading Images to Server***
``` terminal
for (var img in images) {
 final image = await _fileService.createImage(img['name']!, img['path']!);
 await _sshService.upload(image, img['name']!);
}
```
\
1 - This snippet iterates through the list of images from the previous snippet.\
2 - For each image:\
2.1 - It calls _fileService.createImage() to create a local copy of the image in the application's documents directory. This helps with potential network limitations or caching needs.\
2.2 -  The _sshService.upload() method then uploads the local image file to the server using SFTP (Secure File Transfer Protocol). The specific filename on the server is provided.\
\
``` ```
***
\
***Snippet 3: Creating Local Image Copy***
```terminal
Future<File> createImage(String name, String imagePath) async {
 final directory = await getApplicationDocumentsDirectory();
 final file = File('${directory.path}/$name');
 final imageData = await rootBundle.load(imagePath);
 final bytes = imageData.buffer
     .asUint8List(imageData.offsetInBytes, imageData.lengthInBytes);
 file.writeAsBytesSync(bytes);
 return file;
}
```
\
1 This function, createImage, takes the image name and path within the application's assets as input.\
2 It retrieves the application's documents directory and creates a file path for the local copy of the image.\
3 It then loads the image data from the provided path using rootBundle.load().\
4 The code extracts the raw byte data from the loaded image.\
5 Finally, it writes the byte data to the newly created local file.\
\
``` ```
***
\
***Snippet 4: Uploading File to Server***
```terminal
/// Connects to the current client through SFTP, uploads a file into it and then disconnects.
upload(File inputFile, String filename) async {
 Future.delayed(const Duration(seconds: 3));
 try {
   bool uploading = true;
   final sftp = await _client?.sftp();
   final file = await sftp?.open('/var/www/html/$filename',
       mode: SftpFileOpenMode.truncate |
           SftpFileOpenMode.create |
           SftpFileOpenMode.write);
   var fileSize = await inputFile.length();
   file?.write(inputFile.openRead().cast(), onProgress: (progress) {
     if(fileSize == progress){
       uploading = false;
     }
   });
   if(file==null){
      print('null');
      return;
   }
   await waitWhile(() => uploading);
 } catch (error) {
   if (kDebugMode) {
     print(error);
   }
 }
}
```
\
1 - This function, upload, handles uploading a file to the server via SFTP.\
2 - Try to establish an SFTP connection and open a file on the server with write permissions.\
3 - Retrieves the size of the local file.\
4 - It reads the contents of the local file in chunks and writes it to the open file on the server. It also includes a 
progress tracking mechanism.\
5 - Error handling is included:\
5.1 - If the server file cannot be opened, log a message.\
5.2 - If any other error occurs during loading, log the error if debug mode is enabled.\
\
``` ```
***
\
***Overall, these snippets work together to:***\
\
→ Prepare data for visualization (KML including placemark and images).\
→ Create local copies of images on the device if needed.\
→ Upload the images to a server using SFTP.\
\
This facilitates displaying the images and associated information on a Liquid Galaxy system for interactive visualization.\
\
→ [https://pub.dev/packages/path_provider](https://pub.dev/packages/path_provider)\
→ [https://github.com/TerminalStudio/dartssh2](https://github.com/TerminalStudio/dartssh2)









