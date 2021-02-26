# Hi3521DV100
720p camera used. H264BSAnalyzer is recommeded to analyse the coded H264 file

## **1. H264 stream process:**

Open sample_vio.c 
The main process flow:VI->VENC->VPSS->VDEC->VO

## **2. Performance compared with Intel QSV, KungPeng920**
 command:
 ```QSVEncC64 --fps 25 --input-res 1280x720 --qvbr 1040 -i "AVBR.yuv" -o "AVBR.h264" ```
 
 dependency: Intel HD Graphics 520；Media SDK Hardware API v1.19；QSVEnc 3.33

<img src="https://github.com/zdszx/Hi3521DV100-/blob/master/IMAGE/QSV.png" width="500" height="400" /><br/>

 command:
 ``` ffmpeg -f rawvideo -pix_fmt yuv420p -s 1280x720 -r 25 -i 6_AVBR.yuv -c:v libx264 -f rawvideo out2_AVBR.h264```
 
 dependency: ffmpeg4.2.1；x264 ENClibrary
 
![image](https://github.com/zdszx/Hi3521DV100-/blob/master/IMAGE/kp920.png)
 
### Result:
 
![image](https://github.com/zdszx/Hi3521DV100-/blob/master/IMAGE/3.png)

![image](https://github.com/zdszx/Hi3521DV100-/blob/master/IMAGE/4.png)

The H264 encoding done by ffmpeg on the Kunpeng 920 differs from the frame structure of the Hi3521 encoded file, firstly, its entropy encoding method is CABAC, the bit rate of CABAC saves 5%-14% compared to CAVLC, and the bit rate saving increases with the increase of quantization step. its computational resource consumption is acceptable on server-level CPUs.

GPU encoding provides separate image information PPS and SEI for each frame's pixel matrix, thanks to its suitability for computationally intensive tasks, but because of the low performance of control-intensive tasks during video encoding (slow exchange between GPU and computer main memory), QSV also does not make the work pipeline between CPU and GPU. it shows low performance of control-intensive tasks in the video encoding process.

## **3. H264toRTPsend / RTPtoH264recv:**

send command:
```./send_h264file_rtp  -t|u [send via tcp(default) or udp]  [h264filename]  [IP]127.0.0.1  [PORT]1234```

recv command:
```./recv   [save filename]  [PORT]```

![image](https://github.com/zdszx/Hi3521DV100-/blob/master/IMAGE/1.png)
