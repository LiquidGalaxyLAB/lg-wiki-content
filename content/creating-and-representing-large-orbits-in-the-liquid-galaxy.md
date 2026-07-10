---
title: Creating and representing large orbits in the Liquid Galaxy
contributor: Mattia Baggini
date: 2024-06-06T08:24:31.671+00:00
---

_**About**_
-----------

  
The aim of this research is to determine how far orbits can be handled and comfortably displayed on Google Earth.  
  

* * *

_**Representation**_
--------------------

  
To represent the orbit, I downloaded the orbit data (TLE) from [N2YO.com](https://www.n2yo.com/), generated the KML file from it and uploaded it to Google Earth Pro 7.3.6.9750 (64-bit).  
  

* * *

_**Results**_
-------------

  
After some testing, I found out that the **maximum altitude** of an orbit displayed on Google Earth is **approximately** 36.000 km (~22.369 miles).  
  
In this research all altitude values are considered **Absolute** type. Let's look at the Graveyard orbit below, which has an altitude of 36.050 km.  
  
![Graveyard_Orbit](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh1rMF0zEs4hiLRX8C0B425-kGP7Gg4Q9ge670wBGPCCUVVkc5w4ppnhblAq6sDjE1KoZ56OxVv1qRSPekErDGsbvMqfRzj2llJ2EutOh7M8gtF1VuCm1YJVn759oyTQqrUbBd2GBy4z-O_bO1hUk-ZLBLS_1meQPuSCBcZ3pNkJpaFOGlfKhSjeMpwX-In/s320/Graveyard_Orbit.png "Graveyard_Orbit")  
[Graveyard Orbit](https://www.satnow.com/community/what-do-you-mean-by-graveyard-orbit#:~:text=A%20graveyard%20orbit%20is%20an,satellites%20and%20generating%20space%20debris.)  
  
This is because the camera altitude can reach a **maximum** of 63.000 km and cannot be extended natively in Google Earth.  
  
![altitude](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhNSSl7Shsi2XGsdzhKGN9fCsO5Wsr_XPnAv_0CokQbvpyL97FeDUSwosdg1awuLvip81rd51gvyj8cPtkXtaS1H4EsYniQMCmTpcER4QNVDyG8xjjaJIZ5CeGdNzbTLdb98Nj8va2rvQk79423j26yIZ2UP_FLudwYwqHm_CyiMr7PhrJZnERrn4F1HQun/s320/altitude.png "altitude")  

* * *

_**Considerations**_
--------------------

  
So now we understand that orbits can be represented at an altitude of approximately 36.000 km. It's important to keep in mind that this value may vary due to altitude changes during the orbit. Let's take the GPS orbit as an example:  
  
![navstar](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi6-SnITEgkRwBVw6_BE_UdTGNBXkgwKO_9ersF_2KuEK9ofPOrxC-xnGlfNBDMKJ38T4GaLWsYGDARy8coXgcycEv2x0jPccE251LPskytHo9SbVgU4Kyay0ODJ1gIfDLcKSabs_eH2ssoWcPH-jzF2xiDx44q1RDCtH1L9CitE9GfFb6O-2n0CNy226Xs/s320/navstar.png "navstar")  
[NAVSTAR 81 (USA 319) (GPS)](https://www.n2yo.com/satellite/?s=48859)  
In the elevation profile, we can see the variations in elevation over time.  
  
![navsta_altitude](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi1Cn13mmhkwxujM3E5tfWwIZM7vRnrmZwU4zco1mZ4pttPDL2tLGy6ucMJuGnpTgxxPekjf2SJ603I2ZU44jq4BsyLz_4hleGCAUJtA5sDfNQ9JF2mvnTR3JV5kqHWUp8DBhI0BsbDyutva2Nm_1546ExOS3loHtEk_4hs2ufwM3suvkUVDyARqLNIeRGH/s320/navsta_altitude.png "navsta_altitude")  

* * *

_**Another example (QZSS orbit)**_
----------------------------------

  
![qzss](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiYgV7EFJaFqplPaSNUXf85KpOgomTWIgftbv21mMe9SMOowcuEH64ScRwO24VZDqfpKPmnS9CZ_9RLqflrh9h7yNtRjJyBMYtHLMgYLLLlXTNwzlR4rEN9vXa8dx_6IA9CJkX6TyteUxGqNALlWjrvi6d0jWWpBjEJKWqC51n6r20AYtaNdsYRuM7ffIPx/s320/qzss.png "qzss")  
[QZS-4 (MICHIBIKI-4)](https://www.n2yo.com/satellite/?s=42965)  
With that, we can represent all orbits in a realistic way (keeping in mind the altitude limits).  
  
  
**That’s all!**  
written by Mattia Baggini
