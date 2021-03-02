send_h264file_by_rtp
====================

test:

```console
$ make
$ make test

$ # cvlc test.sdp &  # or mplayer(or ffplay) test.sdp &
$ # ./send_h264file_rtp record.h264 127.0.0.1 1234
```
send command:
```./send_h264file_rtp  -t|u [send via tcp(default) or udp]  [h264filename]  [IP]127.0.0.1  [PORT]1234```

recv command:
```./recv   [save filename]  [PORT]```

![image](https://github.com/zdszx/Hi3521DV100-/blob/master/IMAGE/1.png)

