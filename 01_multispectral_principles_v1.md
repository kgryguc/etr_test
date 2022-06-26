# Prerequisites

For working on this theme, you need:  
- basic knowledge of QGIS  
- basic knowledge of remote sensing data resolution

# Principles of multispectral imaging

Presentation of multispectral data characteristics and their potential
in environmental applications.

## Objectives

In this theme, you will learn about:

-   …  
-   …

After finishing this theme you will be able to visualise multispectral
data and spectral characteristics for different objects from different
sensors and to calculate selected vegetation indices.

## Spectral ranges in optical domain

***(bridge with Module 1 - content to be agreed)***

## Use of different ranges

***(bridge with Module 1 - content to be agreed)***

## Selected sensor characteristics

***(bridge with Module 1 - content to be agreed)***

-   MODIS, Landsat, Sentinel, PlanetScope, RapidEye…  
-   RGB composites, visualisation

<div>

<b>Table 1. Selected satellite sensor characteristics.</b>

</div>

|     Satellite     |                             Sensor                             |     Abbreviation     |                    Spectral range (µm)                    |             Pixel size (m)             | Swath width (km) |
|:-----------------:|:--------------------------------------------------------------:|:--------------------:|:---------------------------------------------------------:|:--------------------------------------:|:----------------:|
|       Aqua        |         Moderate Resolution Imaging Spectroradiometer          |        MODIS         |         VNIR+SWIR (0,40-2,155), TIR (3,66-14,28)          |                250-1000                |       2330       |
|   Landsat 1/2/3   |                      Return Beam Vidicon                       |         RBV          |                     VNIR (0,47-0,83)                      |                80/80/80                |       185        |
| Landsat 1/2/3/4/5 |                     Multispectral Scanner                      |         MSS          |                     VNIR (0,50-1,10)                      |              80/80/40/80               |       185        |
|    Landsat 4/5    |                        Thematic Mapper                         |          TM          |                   VNIR+SWIR (0,45-2,35)                   |                 30/30                  |       185        |
|     Landsat 7     |                 Enhanced Thematic Mapper Plus                  |         ETM+         | PAN (0,52-0,90), VNIR+SWIR (0,45-2,35), TIR (10,40-12,50) |      15 (PAN), 30 (MS), 60 (TIR)       |       185        |
|     Landsat 8     |                    Operational Land Imager/                    |       OLI/TIRS       | PAN (0,50-0,68), VNIR+SWIR (0,43-2,29), TIR (10,60-12,51) |      15 (PAN), 30 (MS), 100 (TIR)      |       185        |
|     Landsat 9     |                   Operational Land Imager 2                    |         OLI2         | PAN (0,50-0,68), VNIR+SWIR (0,43-2,29), TIR (10,30-12,50) |      15 (PAN), 30 (MS), 100 (TIR)      |       185        |
|    Pleiades-1     |                    High-Resolution Imager-                     |        HiRI-         |             PAN (0,47-0,83), VNIR (0,43-0,94)             |           0,5 (PAN), 2 (MS)            |        20        |
|    PlanetScope    |                      PS2, PS2.SD, PSB.SD-                      | PS2, PS2.SD, PSB.SD- |                     VNIR (0,45-0,86)                      |                   3                    |        24        |
|     RapidEye      |                 RapidEye Earth-imaging System-                 |        REIS-         |                     VNIR (0,40-0,85)                      |                   5                    |        77        |
|    Sentinel-2     |                    Multispectral Instrument                    |         MSI          |                   VNIR+SWIR (0,44-2,20)                   |               10–60 (MS)               |       290        |
|    SPOT 1/2/3     |                    High Resolution Visible                     |         HRV          |             PAN (0,51-0,73), VNIR (0,50-0,89)             |           10 (PAN), 20 (MS)            |        60        |
|      SPOT 4       |                High Resolution Visible Infrared                |        HRVIR         |          PAN (0,61-0,68), VNIR+SWIR (0,50-1,75)           |           10 (PAN), 20 (MS)            |        60        |
|      SPOT 5       |                  High Resolution Stereoscopic                  |         HRS          |                      PAN (0,48-0,70)                      |                  5–10                  |       120        |
|      SPOT 5       |                   High Resolution Geometric                    |         HRG          |          PAN (0,48-0,71), VNIR+SWIR (0,50-1,75)           |        2,5-5 (PAN), 10-20 (MS)         |        60        |
|     SPOT 6/7      |            New AstroSat Optical Modular Instrument             |        Naomi         |             PAN (0,45-0,75), VNIR (0,45-0,89)             |           1,5 (PAN), 6 (MS)            |        60        |
|       Terra       | Advanced Spaceborne Thermal Emission and Reflection Radiometer |        ASTER         |          VNIR+SWIR (0,52-2,43), TIR (8,12-11,65)          |          15-30 (MS), 90 (TIR)          |        60        |
|                   |         Moderate Resolution Imaging Spectroradiometer          |        MODIS         |         VNIR+SWIR (0,40-2,155), TIR (3,66-14,28)          |                250-1000                |       2330       |
|     QuickBird     |                Ball Global Imagery System 2000-                |      BGIS2000-       |             PAN (0,45-0,90), VNIR (0,45-0,90)             |    0,65-0,73 (PAN), 2,62-2,92 (MS)     |     16,8/18      |
|    WorldView-2    |                      WorldView-110 camera                      |        WV110         |             PAN (0,45-0,80), VNIR (0,40-1,04)             |          0,46 (PAN), 1,8 (MS)          |       16,4       |
|    WorldView-3    |                      WorldView-110 camera                      |        WV110         | PAN (0,45-0,80), VNIR+SWIR (0,40-2,36), CAVIS (0,40-2,24) | 0,31 (PAN), 1,24-3,70 (MS), 30 (CAVIS) |       13,1       |
|    WorldView-4    |                      SpaceView-110 camera                      |        WV110         |             PAN (0,45-0,80), VNIR (0,45-0,92)             |         0,31 (PAN), 1,24 (MS)          |       13,1       |

## Spectral indices

***(bridge with Module 1 - content to be agreed)***

-   concept  
-   calculation

## Advantages and limitations of satellite multispectral imaging

The use of many spectral bands allows for wider interpretation and
analysis possibilities of objects than in the case of RGB photographs.
Having **red-edge, near and mid-infrared** bands strengthens them even
more in **vegetation analyses**. The width of the spectral bands is of
great importance here, which varies depending on the sensor (see
comparison between Landsat 7 and 8 bands with Sentinel-2 in [Theme 1 in
Module
1](#../../module1/01_principles_of_remote_sensing_time_series/01_principles_of_remote_sensing_time_series.md).

Satellite level of data acquisition has the advantage that it is
possible to acquire scenes with regular temporal resolution of images,
which allows to fully explore their potential in multitemporal analyses.
The limitation, however, is that despite the cyclical nature of data
acquisition, it happens that for a selected area for a long time it is
not possible to find cloudless imagery, for data provided free of
charge, which is performed at a specific interval, and not on request.
However, for the latter, this can also be a challenge.

**Table 2** lists the main pros and cons of satellite multispectral
image data acquisition in general, however it is obvious that individual
missions differ in technical parameters, which is presented in Table 1
above. Multispectral data can also be obtained from the airborne or UAV
level, similarly, hyperspectral data in planned missions are to be
obtained from the satellite platforms, but since this Module deals with
multispectral satellite data, the information in the table applies to
them.

<div>

<b>Table 2. Advantages and limitations of satellite multispectral
imaging.</b>

</div>

|                        Advantages                         |                Limitations                 |
|:---------------------------------------------------------:|:------------------------------------------:|
|          data acquisition anywhere on the globe           |                 pixel size                 |
|               source of big archive of data               |     the need of atmospheric correction     |
|                   real-time collection                    |            occurence of clouds             |
|                coverage of extensive area                 |    irregularly spaced bands, often wide    |
| relatively fast pre-processing due to the number of bands | high cost for high spatial resolution data |
|                    regular overflights                    |                                            |
|                   some freely available                   |                                            |
|     spectral ranges including VNIR and some also SWIR     |                                            |
|                 repeatability of analysis                 |                                            |
|                    missions continuity                    |                                            |

## Multispectral satellite data archives

***(bridge with Module 1 - content to be agreed)***

The wide range of Earth observation missions by various government
agencies and private companies means that the **number of available
sources with access to satellite data is increasing every year**. The
vast amount of information requires that the data be properly catalogued
and offered to the end user in as simple a form as possible so that they
can easily find the data relevant to the applications and effects they
wish to obtain. It also offers access to the computing power to find,
process, and analyse multi-temporal (and sometimes multi-sensor)
collections in some cases within a single platform. The large data
archive services of major national and international government agencies
such as NASA or ESA and the major private companies that provide cloud
space and computing power are filled with data from many different
missions. Smaller archives often offer more specialised data from
smaller satellite missions or processed to a level that allows analysis
in selected areas.

Data available in archives can be divided by several characteristics.
Archives offering free access are most often projects of agencies (that
own the satellites), universities, and enthusiast communities.
Commercially available data are owned by companies that operate private
satellites and repositories of data from them. Some of the preprocessed
Analysis Ready Data may also sometimes be available for a fee.
Commercial parties often offer a free sample of data or a trial plan to
get you acquainted with the service. All services may offer tools for
**searching, browsing, downloading, processing and analysing data**.
Some offer multiple functionalities simultaneously. Depending on the
user’s needs and level of sophistication, they can be operated using a
graphical interface or, in some cases, also using a programming console
and API. Large fragmentation and multiplicity of possibilities, apart
from many advantages of such a solution, also make it necessary to spend
time on selection of appropriate sources, which may require creating
multiple accounts in different services and the necessity of learning
how to use them.

The Table 3 below consists of multiple different purposes and content
platforms available in English containing optical satellite imagery. We
chose to present archives not related to just one area or missions,
albeit those services can be useful for a specific purpose. Short list
of such platforms can be found below.

<div>

<b>Table 3. Selected satellite data platforms.</b>

</div>

| Company/agency                                                  | Platform (site)                                                                | Description                                                                                                                                                      | Quick links                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Open | Commercial (free samples) | Visualize | Download | Analysis | Imagery sources/satellites                                                                                                                                                                                                           | Notes                                                                 |
|-----------------------------------------------------------------|--------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------|---------------------------|-----------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| [Amazon](https://www.aboutamazon.com/)                          | [Amazon Web Services Earth](https://aws.amazon.com/earth/)                     | Cloud computing platform offering various ranges of data and services.                                                                                           | [REGISTRATION](https://portal.aws.amazon.com/billing/signup?nc2=h_ct&src=header_signup&redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start/email) [LOGIN](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Fus-east-1.console.aws.amazon.com%2Fconsole%2Fhome%3FhashArgs%3D%2523%26isauthcode%3Dtrue%26nc2%3Dh_ct%26region%3Dus-east-1%26skipRegion%3Dtrue%26src%3Dheader-signin%26state%3DhashArgsFromTB_us-east-1_e67c8d43f6386ce8&client_id=arn%3Aaws%3Asignin%3A%3A%3Aconsole%2Fcanvas&forceMobileApp=0&code_challenge=-7EUqosuAN20vM4WJTC2QwD0T0wLzWD8jzd2ATzLvaQ&code_challenge_method=SHA-256) [GETTING STARTED](https://aws.amazon.com/getting-started/)                                                                                                                                                                                                                |      | x                         |           | x        | x        | Sentinel, Landsat, NOAA, SpaceNet, regional datasets.                                                                                                                                                                                | One of the largest data providers/cloud computing services available. |
| [ESA](https://www.esa.int/)                                     | [Copernicus Open Access Hub](https://scihub.copernicus.eu/)                    | Platform provides complete, free and open access to Sentinel mission data.                                                                                       | [REGISTRATION](https://scihub.copernicus.eu/dhus/#/self-registration) [USERGUIDE](https://scihub.copernicus.eu/userguide/)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | x    |                           | x         | x        |          | Sentinel                                                                                                                                                                                                                             | Enables API                                                           |
| [Maxar/European Space Imaging](https://www.euspaceimaging.com/) | [Digital Globe](https://discover.digitalglobe.com/)                            | Browser of products collected by Maxar’s satellites.                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | x    |                           | x         |          |          | WorldView, GeoEye, Quickbird                                                                                                                                                                                                         |                                                                       |
| [USGS](https://www.usgs.gov/)                                   | [EarthExplorer](https://earthexplorer.usgs.gov/)                               | USGS/NASA platform providing tools to search, browse display, export metadata and download data from its vast archive consisting of data reaching 75 years back. | [REGISTRATION](https://ers.cr.usgs.gov/register) [LOGIN](https://ers.cr.usgs.gov/login) [HELP](https://ers.cr.usgs.gov/register)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | x    |                           | x         | x        |          | Landsat, plus MODIS, ASTER. Also open source datasets provided under collaboration with ISRO (Resourcesat-1 and 2), ESA (Sentinel-2), and some commercial high-resolution satellite data (IKONOS-2, OrbView-3, historical SPOT data) | Enables Bulk Download with standalone manager. Enables API.           |
| [GeoCento](https://geocento.com/)                               | [Earthimages](https://geocento.com/earthimages)                                | Platform for ordering high and very high resolution imagery.                                                                                                     | [CONTACT](https://geocento.com/contact)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |      | x                         | x         | x        |          | Landsat, Sentinel, Worldview, SPOT                                                                                                                                                                                                   | Platform for ordering high and very high resolution imagery.          |
| [Sentinel Hub](https://www.sentinel-hub.com/)                   | [EO Browser](https://apps.sentinel-hub.com/eo-browser/)                        | Visualisation, download and simple analysis online platform.                                                                                                     | [EXPLORE](https://www.sentinel-hub.com/explore/eobrowser/) [USER GUIDE](https://www.sentinel-hub.com/explore/eobrowser/user-guide/)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | x    |                           | x         | x        | x        | Landsat, Sentinel, MODIS, ENVISAT, Proba-V                                                                                                                                                                                           | Allows for ordering of private satellite imagery.                     |
| [ESA](https://www.esa.int/)                                     | [EO-Cat](https://eocat.esa.int/sec/#data-services-area)                        | Metadata and imagery browser of Earth Observation data acquired by various satellites.                                                                           | [HELP](https://eocat.esa.int/sec/help.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | x    |                           | x         | x        |          | Envisat, AVHRR, Geosat, JERS-1, Landsat, Proba, Rapideye, Worldview-2                                                                                                                                                                |                                                                       |
| [Airbus](https://www.airbus.com/en)                             | [GeoStore](https://www.intelligence-airbusds.com/geostore/)                    | Platform allowing access for specific satellite missions.                                                                                                        | [REGISTRATION](https://account4.intelligence-airbusds.com/account/CreateAccount.aspx?l=en&RelayState=https://www.intelligence-airbusds.com/) [LOGIN](https://connect4.intelligence-airbusds.com/adfs/ls/?SAMLRequest=rVLBTuMwEP2VyPfUiSmktdpKhQpRiYWKlj3sZTV1ptSSPc56HAp%2FT5ruCrj0tKfRPM978%2Fw0EwbvGj1v056e8E%2BLnLI374h1%2FzAVbSQdgC1rAo%2Bsk9Hr%2BY97rQaFbmJIwQQnvlDOM4AZY7KBRLZcTMXvolLlGNSuqi5hiJUZ4pWpxiNVIKhaFWV1NcaxudgWFyL7iZE75lR0Qh2ducUlcQJKHVQolReXeak2ZamLkVajXyJbdL%2BxBKln7VNqWEtpAhGaNBxYSuicfUEymION25ZrHpjgJdQ7lo6lyOb%2F%2FN4E4tZjXGN8tQafn%2B4%2FFQ%2BHwxkxtr5xeIxG%2BlC3DgfNvpF9z6eqcjDco8fFrQElstXfaK8t1ZZezqe6PQ2xvttsVvnqcb0Rs8lRWfcpxdn%2FcOoxQQ0JvhmdyK9rJqdjeugMLher4Kx5z25D9JDO%2Bz8its53%2FahOEYgtUhJydtL%2Ffp%2BzDw%3D%3D&RelayState=https%3A%2F%2Fwww.intelligence-airbusds.com%2Fuser-login%2F%3Fl%3Den) [HELP](https://www.intelligence-airbusds.com/en/8714-questions-and-answers) |      | x                         |           | x        |          | Pleiades, SPOT, DMC                                                                                                                                                                                                                  |                                                                       |
| [Google](http://about.google)                                   | [Google Cloud Storage](https://cloud.google.com/storage/docs/public-datasets/) | Cloud Storage provides a variety of public datasets that can be accessed by the community and integrated into their applications.                                | [REGISTER](https://accounts.google.com/signup/v2/webcreateaccount?service=cloudconsole&continue=https%3A%2F%2Fconsole.cloud.google.com%2Ffreetrial%3F_ga%3D2.48750438.1590195550.1652279703-232008209.1604320050&dsh=S1326015960%3A1652353991880874&biz=false&hl=en-GB&flowName=GlifWebSignIn&flowEntry=SignUp&nogm=true) [HELP](https://cloud.google.com/storage/docs/support)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | x    |                           |           | x        |          | Sentinel-2, Landsat                                                                                                                                                                                                                  | Enables API.                                                          |
| [Google](http://about.google)                                   | [Google Earth](https://earth.google.com/web/)                                  | Visualisation of the whole globe on many levels of detail.                                                                                                       | [RESOURCES](https://www.google.pl/intl/pl/earth/resources/)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | x    |                           | x         |          |          |                                                                                                                                                                                                                                      | Available in the Web browser, and as a stand alone PC and mobile app. |
| [Google](http://about.google)                                   | [Google Earth Engine](https://earthengine.google.com/)                         | A planetary-scale platform for Earth science data & analysis.                                                                                                    | [FAQ](https://earthengine.google.com/faq/) [PLATFORM INFORMATION](https://earthengine.google.com/platform/)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | x    |                           | x         | x        | x        | Landsat, Sentinel, MODIS                                                                                                                                                                                                             | Enables API.                                                          |
| [EOS](https://eos.com/)                                         | [Landviewer](https://eos.com/landviewer/)                                      | Satellite observation imagery tool that allows for on-the-fly searching, processing and getting valuable insights from satellite data.                           | [USER GUIDE](https://eos.com/products/landviewer/user-guide/)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |      | x                         | x         | x        | x        | Landsat, Sentinel, SPOT, Pleiades                                                                                                                                                                                                    |                                                                       |
| [Microsoft](https://www.microsoft.com/)                         | [Microsoft Planetary Computer](https://planetarycomputer.microsoft.com/)       | Data archive platform with expanding functionalities.                                                                                                            | [ABOUT](https://planetarycomputer.microsoft.com/docs/overview/about)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |      | x                         |           | x        |          | Landsat, Sentinel, ASTER                                                                                                                                                                                                             | Enables API.                                                          |
| [Airbus](https://www.airbus.com/en)                             | [OneAtlas](https://oneatlas.airbus.com/)                                       | Airbus satellite images and add maps enabled by ordering features.                                                                                               | [TUTORIALS](https://api.oneatlas.airbus.com/tutorials/t-explore-data/)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |      | x                         |           | x        |          |                                                                                                                                                                                                                                      | Enables API.                                                          |
| [Sentinel Hub](https://www.sentinel-hub.com/)                   | [Sentinel Playground](https://apps.sentinel-hub.com/sentinel-playground/)      | A free to use web application that allows for rapid online viewing and access to image archives.                                                                 | [INFORMATION](https://www.sentinel-hub.com/explore/sentinelplayground/)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | x    |                           | x         |          |          | Landsat, Sentinel, MODIS                                                                                                                                                                                                             |                                                                       |

## Exercise

Object identification, image interpretation and spectral properties
analysis in [QGIS](../../software/software_qgis.md).

### Next unit

Proceed with [Temporal information in satellite
data](../02_temporal_information/02_temporal_information.md)
