---
title: Migration from pub.dev ssh to dartssh2 with version 3.x of flutter
contributor: Gerard Monsó
date: June 10, 2024
---

  
_**Introduction**_  
  
Each entry has to have the clearest definition of what the entry is, and what part of the Liquid Galaxy handles, it can be UX side (functions on the apps in Flutter or JAVA) or the rig side (all the things related to the Liquid Galaxy cluster and his network, including the AI server and the Dockers we use).  
Please write with clarity for others to understand, and quote code in the right way. Add graphics if needed, and remember to store the images in the same folder independently.  
TIP: it's better that you send us a previous email with what 3 contents you want to create for the wiki, as many other contributors may have chosen the same.  
Each entry has to be a minimum of half a page, as you have to explain the aforementioned parts and the code or instructions involved.  
You’ll be credited if the entry is published, and also you can be invited to write other ones if the ones you choose have been already written many times.  
Send proof of this task to liquidgalaxylab@gmail.com with the link of the shared Google Drive folder, with open-to-anybody link permissions as mentors will need access to it. Have this folder ready for all the processes.  
Please name the doc with your name and GSoC2024. We’ll not accept pdfs or .docx Drop too a DM to admins in our Discord saying the doc is ready.  
  
→ Migration from pub.dev ssh to dartssh2 with version 3.x of flutter  
→ key points for installing the LG that generate the most common errors.  
→ Sending images about a real LG machine.  
  

* * *

  
Hello community!  
I'm reaching out today to discuss a topic that gave me major headaches during my recent migration from Flutter 3: Migration from pub.dev ssh to dartssh2 with version 3.x of flutter. This particular aspect caused quite a stir, and I'm hoping to help others avoid similar struggles.  
  

* * *

  
_**Comparison of dartssh vs. dartssh2**_  
  
dartssh and dartssh2 are two Flutter packages that allow interaction with SSH and SFTP servers. However, there are some key differences between them:  
dartssh:  
→ Implementation: Uses platform-native libraries (NMSSH for iOS and JSch for Android).  
→ Maintenance: No longer actively maintained for 3 years and has known issues.  
→ Compatibility: Not compatible with Dart 3.  
→ License: MIT  
  
dartssh2:  
→ Implementation: Written entirely in Dart, making it more portable and free of native platform dependencies.  
→ Maintenance: Actively maintained and frequently updated.  
→ Compatibility: Compatible with Dart 3.  
→ License: MIT  
  
![dartssh2](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEie3hu8FZaYF0fjgWvyClSXst_YCotV4jVb-MocCnSNy-za5WxrJ8e34ocRfOWI9R-XxTMTYWy23SPgw1CG14od34aa8nuWDzStSt4RdjRuV1NrvQ8HVdgmAiZtvO9J-4evC43nYllp4358ZtDQn_9tDWRrUdmuCE5mmx-3iIWW0-PE3Gey_KnsZc9jWxkC/s1600/dartssh2.png "dartssh2")  

* * *

  
_**Migrating from dartssh to dartssh2**_  
  
If you are currently using dartssh in your Flutter project, it is recommended to migrate to dartssh2 to take advantage of its benefits and avoid compatibility and maintenance issues.  
## Here are some general steps for the migration:
  
→ Replace the dependency: In your pubspec.yaml file, replace the ssh dependency with dartssh2.  
  
→ Update imports: Update imports from package:ssh/ssh.dart to package:dartssh2/dartssh2.dart in your code files.  
  
→ Code adjustments: Keep in mind that the dartssh2 API differs slightly from dartssh. You may need to review the dartssh2 documentation and make minor adjustments to your code to adapt it to the new API.  
  
**For a more detailed guide on migration and API differences, it is recommended to consult the documentation of both packages:**  
  
→ ssh: [https://pub.dev/packages/ssh](https://pub.dev/packages/ssh)  
→ dartssh2: [https://pub.dev/packages/dartssh2](https://pub.dev/packages/dartssh2)  
  
Keep in mind that this is a general guide and you may need to adapt the process to your specific project. If you encounter difficulties during the migration, you can consult the Flutter community resources or seek help from an experienced developer.  
  
→ [https://github.com/TerminalStudio/dartssh2](https://github.com/TerminalStudio/dartssh2)  
→ [https://github.com/shaqian/flutter\_ssh](https://github.com/shaqian/flutter_ssh)
