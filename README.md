# Image-Stitching-Tanpa-MPI
# Sebelum Bekerja
>*Lakukan Step Ini di Windows dan Ubuntu Desktop*

1. Buatlah sebuah folder yang berisikan potongan-potongan gambar, kodingan python dan juga output gambar.

   Windows:

   ![image](https://github.com/nabillasuci24/Image-Stitching-Tanpa-MPI/assets/150004555/396e37bc-d0ec-477c-8f02-c6a4063f9bd6)

    Ubuntu Desktop:

    ![image](https://github.com/nabillasuci24/Image-Stitching-Tanpa-MPI/assets/150004555/ed7610a7-905e-40cb-b1ab-f62062981012)

    Gambar yang Digunakan:

     ![image](https://github.com/nabillasuci24/Image-Stitching-Tanpa-MPI/assets/150004555/0751285f-fab0-4cab-95d5-3cf50ec7bc5a)

     ![image](https://github.com/nabillasuci24/Image-Stitching-Tanpa-MPI/assets/150004555/bd042768-80c6-4243-9bcc-88d59ee191a3)

     ![image](https://github.com/nabillasuci24/Image-Stitching-Tanpa-MPI/assets/150004555/77a32400-883a-40e0-bc7a-72c6729f24c1)

     Output:

     ![image](https://github.com/nabillasuci24/Image-Stitching-Tanpa-MPI/assets/150004555/a020ed5d-5fb9-4ddb-84bc-af4eb08fab65)

    Program atau Kodingan Python yang Saya Gunakan:
   ```sh
    # USAGE
    # python image_stitching_simple.py --images images/scottsdale --output output.png

    # import the necessary packages
    from imutils import paths
    import numpy as np
    import argparse
    import imutils
    import cv2

    # construct the argument parser and parse the arguments
    ap = argparse.ArgumentParser()
    ap.add_argument("-i", "--images", type=str, required=True,
            help="path to input directory of images to stitch")
    ap.add_argument("-o", "--output", type=str, required=True,
            help="path to the output image")
    args = vars(ap.parse_args())
   
    # grab the paths to the input images and initialize our images list
    print("[INFO] loading images...")
    imagePaths = sorted(list(paths.list_images(args["images"])))
    images = []

    # loop over the image paths, load each one, and add them to our
    # images to stich list
    for imagePath in imagePaths:
            image = cv2.imread(imagePath)
            images.append(image)

    # initialize OpenCV's image stitcher object and then perform the image
    # stitching
    print("[INFO] stitching images...")

    # Create a Stitcher with a default ORB (feature-based) detector
    stitcher = cv2.Stitcher_create(cv2.Stitcher_SCANS)

    # Detect keypoints and set camera parameters manually
    status, stitched = stitcher.stitch(images)
    if status != cv2.Stitcher_OK:
        print("[INFO] Camera parameters adjustment failed. Retrying with manual adjustment...")
    
        # Manually set camera parameters
        stitcher.setWarper(cv2.detail_WaveCorrectKind_HORIZ)
        stitcher.setWaveCorrection(True)
        stitcher.setFeaturesFinder(cv2.Stitcher_createFeaturesFinder())
    
        # Retry stitching
        status, stitched = stitcher.stitch(images)

    # print additional information
    print("[INFO] Stitching Status:", status)

    # if the status is '0', then OpenCV successfully performed image
    # stitching
    if status == cv2.Stitcher_OK:
        # write the output stitched image to disk
        cv2.imwrite(args["output"], stitched)

        # display the output stitched image to our screen
        cv2.imshow("Stitched", stitched)
        cv2.waitKey(0)

    # otherwise, the stitching failed
    else:
        print("[INFO] image stitching failed ({})".format(status))

        # print additional information
        if status == cv2.Stitcher_ERR_NEED_MORE_IMGS:
            print("[INFO] Need more images for stitching.")
        elif status == cv2.Stitcher_ERR_HOMOGRAPHY_EST_FAIL:
            print("[INFO] Homography estimation failed.")
        elif status == cv2.Stitcher_ERR_CAMERA_PARAMS_ADJUST_FAIL:
            print("[INFO] Camera parameters adjustment failed.")
        elif status == cv2.Stitcher_ERR_MATCH_CONFIDENCE_FAIL:
            print("[INFO] Match confidence test failed.")
        elif status == cv2.Stitcher_ERR_CAMERA_PARAMS_VERIFY_FAIL:
            print("[INFO] Camera parameters verification failed.")

    # ... (existing code)
    ```

2. Instalasi pustaka-putsaka seperti imutils, numpy dan opencv-python dengan command
'pip install imutils'
'pip install numpy'
'pip install opencv-python'
pada cmd dan juga ubuntu desktop.

![image](https://github.com/nabillasuci24/Image-Stitching-Tanpa-MPI/assets/150004555/674cfaea-d0cf-42a8-9e0b-d3255462f241)

![image](https://github.com/nabillasuci24/Image-Stitching-Tanpa-MPI/assets/150004555/083e0c76-da68-484f-94e8-ab2886765f58)

  # A. Image Stitching Pada VSCode
  ## 1. Buka folder yang telah kita buat di awal pada VSCode

    ![image](https://github.com/nabillasuci24/Image-Stitching-Tanpa-MPI/assets/150004555/de7998f2-3807-4eca-9d3f-73f4df59a03a)

    ![image](https://github.com/nabillasuci24/Image-Stitching-Tanpa-MPI/assets/150004555/39c11d25-d1b1-48a0-b0f1-029f4783b41e)


  ## 2. Kemudian jalankan kodingan tersebut dan akan muncul output pada terminal seperti di bawah, lalu ketikan di terminal 'python image_stitching_simple.py –images images –output output.png'. Maka akan muncul hasil dari stitching image.

    ![image](https://github.com/nabillasuci24/Image-Stitching-Tanpa-MPI/assets/150004555/cea0a506-4d83-4a32-96b6-ab7258a24554)

  # B. Image Stitching pada CMD
  ## 1. Masuk ke direktori dengan command 'cd C:\Laporan 5 PemPar' (tempat lokasi folder disimpan dan juga nama folder yang telah di buat di awal).
  ## 2. Kemudian, ketik command 'python image_stitching_simple.py –images images –output output2.png'. Maka akan muncul hasil dari stitching image.

  ![image](https://github.com/nabillasuci24/Image-Stitching-Tanpa-MPI/assets/150004555/1ac0cf96-6971-4aed-918e-e37ca7773cde)

  # C. Image Stitching pada Ubuntu Desktop
  ## 1. Pastikan Ubuntu kalian sudah ter update dan upgrade versi terbaru, bisa menggunakan command 'sudo apt update' dan 'sudo apt upgrade'.

  ![image](https://github.com/nabillasuci24/Image-Stitching-Tanpa-MPI/assets/150004555/6d347770-3a7e-4b40-8d7d-3cef70b7a888)

  ## 2.	Install Python3 dengan command 'sudo apt install python3-pip'

  ![image](https://github.com/nabillasuci24/Image-Stitching-Tanpa-MPI/assets/150004555/893460e7-bbd4-400a-8001-3a4c93087cdd)

  ## 3.	Masuk ke direktori dengan command 'cd Downloads\Lapor5' (tempat penyimpanan folder dan nama folder yang kita buat di awal). 
  ## 4.	Setelah masuk ke direktori ketik command 'python image_stitching_simple.py –images images –output output3.png'. Maka akan muncul hasil dari stitching image.

  ![image](https://github.com/nabillasuci24/Image-Stitching-Tanpa-MPI/assets/150004555/d1770a76-2002-43e3-9752-30f0aea8e07f)
