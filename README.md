# Hi3521DV100
720p camera used. H264BSAnalyzer is recommeded to analyse the coded H264 file

H264 stream process:

Open sample_vio.c 

The main process flow:VI->VENC->VPSS->VDEC->VO


H264toRTP send/RTPtoH264recv:

./send_h264file_rtp  -t|u [send via tcp(default) or udp]  [h264filename]  [IP]127.0.0.1  [PORT]1234

./recv   [save filename]  [PORT]
