# tokyo-localization-2022 dataset

## Dataset Description
---

The tokyo-localization-2022 dataset is a set of query images taken in Tokyo and the ground-truth pose of query images based on 3D mesh model PLATEAU[^1]. If you use the dataset, you must agree to the terms of dataset license below.

[^1]: PLATEAU: https://www.mlit.go.jp/plateau/

## **Overview**
---

Our tokyo-localization-2022 dataset contains the followings.

1. 63 query images .
2. Ground-truth poses (i.e., the position and rotation in 3D mesh model) of the query images.
3. Geo-tag data (latitude, longitude, altitude, and azimuth obtained from geomagnetic sensors) of the query images when they was taken and intrinsic parameters of the camera.

In addition, out dataset contains the following ***metadata*** for rendering images from PLATEAU. This is the experimental data we used for our reference examination "Pre-rendering".

4. Camera poses (i.e., the position and rotation in 3D mesh model)  and intrinsic parameters for rendering images.

## **Details of the query image and associated data for the query image**
---

The query images are contained in the ZIP file in the tokyo-localization-2022/query directory.
Associated data (query image list, Ground-truth pose, Geo-tag data and intrinsic parameters of the camera) are contained each npy files in the same directory.

The Query image list file contains the file names of the images.
Each associated data file contains each data in the same order as the query image list.

For example, if you want to obtain the geo-tag data for IMG_0404.JPG, you can do so as follows.

    ```
    import numpy as np

    query_list = np.load("tokyo-localization-2022/query/query-list.npy")
    geo-tag = np.load("tokyo-localization-2022/query/geo-tag.npy")
    geo-tag_0404 = geo-tag[query_list=="IMG_0404.JPG"])
    ```

### Ground-truth poses of the query images

The ground-truth poses of query images are the position and rotation in the 3D mesh model and contained in ground-truth.npy file. They are contained in the form of a 3✕4 RT matrix, in the order of the query image list.

### Geo-tag

The geo-tag data of the query images is contained in geo-tag.npy file in the order latitude, longitude, altitude, and azimuth obtained from geomagnetic sensors of the query images. 
The geo-tag data includes latitude, longitude, altitude, and azimuth obtained from geomagnetic sensors. They are listed in this order for each image in the geo-tag.npy file.

### Intrinsic parameters

The intrinsic parameters of the camera taking the query images are the 3✕3 camera matrix and the 5 distortion coefficients and contained in intrinsic_parameters.npy. All query images are taken with the same camera, so it has one set of intrinsic parameters.

## **Details of metadata for the reference examination "Pre-rendering"**
---

Metadata (rendered image list, position of the rendered images, rotaion of the rendered images and the camera poses of rendered images) are contained each npy files in the tokyo-localization-2022/render directory.

The rendered image list file contains the names of the rendered images.
Each metadata file contains each data in the same order as the rendered image list.

For example, if you want to obtain the the poses of rendered images for index_686037330000.png, you can do so as follows.

    ```
    import numpy as np

    image_list = np.load("tokyo-localization-2022/render/image_name.npy")
    RTmat = np.load("tokyo-localization-2022/render/RT_matrix.npy")
    RTmat_686037330000 = RTmat[image_list=="index_686037330000.png"])
    ```

### position and rotaion of the rendered images

The position and rotation of the rendered images in the 3D map are contained in camera_position.npy and camera_rotation.npy, respectively.
The position data is the x,y,z coordinates in the 3D mesh model.
The rotation data is the Euler angle in the x-, y-, and z-axes in the 3D mesh model.

### Camera poses of rendered images

The camera poses of rendered images are contained in RT_matrix.npy. They are the position and rotation in 3D mesh model. They are contained in the form of a 3✕4 RT matrix, in the order of the rendered image list.

## 3D mesh model

PLATEAU can be downloaded from:

https://www.geospatial.jp/ckan/dataset/plateau-tokyo23ku-citygml-2020

Our dataset covers secondary meshes: `533935`, `533936`, `533945`, `533946`. (PLATEAU data can be downloaded by secondary mesh.)

The PLATEAU data you can download from this site is in CityGML format. Please convert this to obj format. In addition, in order to use our dataset, the PLATEAU data must be converted to the plane rectangular coordinates defined by the Ministry of Land, Infrastructure, Transport and Tourism for surveying in Japan. For details on the format and coordinate system conversion, please refer to the official manual below.

https://github.com/Project-PLATEAU/Data-Conversion-Manual-for-3D-City-Model

   - **Note 1.** PLATEAU data is sometimes rotated by default with respect to the plane rectangular coordinate system. The ground-truth and camera pose provided in our dataset were calculated with the rotation angle of the angular axes set to 0 degrees.

## LICENSE AGREEMENT for DATASETS

The following terms comprise the License Agreement for Datasets (the “License Agreement”) made available by the KDDI Research, Inc. (KDDI Research).

### LICENSE

KDDI Research’s authorization to access the data grants you a limited, non-exclusive, non-transferable, non-assignable, and terminable license to copy, modify, and use the data for your research in accordance with this License Agreement. No license is granted for any other purpose and there are no implied licenses in this License Agreement. Nothing in this License is intended to limit any rights you may have arising from fair use or due to other limitations on KDDI Research’s exclusive rights under copyright law or other applicable laws.
You will not disclose the dataset to any other person other than those employed by your institute or organization who are collaborating with you using the dataset.
KDDI Research has the authority and reserves the right, in its sole discretion, to discontinue further access and use to anyone who violates this License Agreement.
If you create a publication (including web pages, papers published by a third party, and publicly available presentations) using data from this dataset, you should cite our paper as follows:

- Title: Recursive Rendering of 2D Images for Accurate Pose Estimation in a 3D Mesh Map
- Authors: Yohei Hanaoka, Suwichaya Suwanwimolkul, Satoshi Komorita
- Venue: SIGGRAPH ASIA 2022, Daegu, South Korea, December 2022


### DISCLAIMER OF WARRANTIES

KDDI Research USES ITS BEST EFFORTS TO PROVIDE DATA IN ACCORDANCE WITH ETHICAL PRINCIPLES AND SCIENTIFIC INTEGRITY. HOWEVER, THE DATA PROVIDED HEREIN IS ON AN “AS IS” BASIS. NEITHER KDDI Research, ITS RESEARCHERS, RESEARCH PARTNERS, LICENSORS, AND DATA PROVIDERS, NOR KDDI Research’s PARENT COMPANY AND ITS OFFICERS, EMPLOYEES, AND AGENTS MAKE ANY WARRANTY, EITHER IMPLIED OR EXPRESS, OF MERCHANTABILITY OR FITNESS FOR A PARTICULAR PURPOSE, INCLUDING, BUT NOT LIMITED TO, THE ACCURACY, TIMELINESS, COMPLETENESS, RELIABILITY, OR AVAILABILITY OF KDDI Research DATA, APPLICATIONS, OR SERVICES ACCESSIBLE THROUGH OR MADE AVAILABLE BY KDDI Research.

### LIMITATION OF LIABILITY

TO THE EXTENT ALLOWED BY LAW, IN NO EVENT SHALL KDDI Research AND ITS PARENT COMPANY BE LIABLE TO YOU OR ANY THIRD PARTY FOR ANY INDIRECT, CONSEQUENTIAL, INCIDENTAL, SPECIAL OR PUNITIVE DAMAGES, ARISING FROM YOUR USE OF THE DATA.
