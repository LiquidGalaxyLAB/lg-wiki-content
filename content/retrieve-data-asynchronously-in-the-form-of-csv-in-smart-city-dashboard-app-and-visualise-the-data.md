---
title: Retrieve data asynchronously in the form of csv  in smart city dashboard app and visualise the data.
contributor: Om Jadhav
date: 2024-06-12T13:57:23.221+00:00
---

  
![visualise the data](https://lh7-us.googleusercontent.com/docsz/AD_4nXf4DGBy6d5AJIhnghvDKYIRZjTzWsfM8O51RRapibjtrQR6krDTEDeYROMvfC3x-F7bX9tIyZ_GsDkA2ZfsLz7fPVijrBCNbCwabBt5xD4meMKoIteuT8bWJ_2eQJLj0uRkIgOxloNyXvQJWRBwXDBze5Q?key=hjiv4J65wMQPabv6eqBdWA "visualise the data")  
→ The data is collected from various sources like Weather API and various sources Like [https://opendata.cityofnewyork.us/data/](https://opendata.cityofnewyork.us/data/) websites.  
→ Data which is in the form of CSV is converted to the Dart data module by processing it.  
→ After the data module is created the data is broken down in small parts to create meaningful information from it i.e the data is parsed.  
→ With the help of this parsed data the flow charts and line charts are created and which are rendered into images.  
→ This rendered images are integrated into KML file  
→ The KML file is send to Liquid galaxy using SSH protocol
