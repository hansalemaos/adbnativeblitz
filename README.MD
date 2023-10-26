# ADB Screenshots as fast as scrcpy, but 100% native!

## Tested against Windows / Python 3.11 / Anaconda

## pip install adbnativeblitz 

AdbFastScreenshots offers a powerful and efficient way to capture 
Android device screens, making it a valuable tool 
for a wide range of applications and use cases.
As fast as https://github.com/hansalemaos/adbblitz , but 100% native! 


## Advantages:

### High Frame Rate: 

AdbFastScreenshots is designed to capture the Android device's screen 
with an improved frame rate, which can be especially useful for applications 
that require real-time or high-speed screen recording, 
such as gaming or performance analysis.

### Efficiency: 

By avoiding the overhead of creating a new subprocess for each screen 
capture session, it is more efficient and less 
resource-intensive than traditional methods, 
making it suitable for continuous screen capture.

### Ease of Use: 

It provides a Pythonic interface for screen capturing, 
making it easier for developers to integrate Android 
screen recording into their applications.

### Control and Flexibility: 

It allows users to control the screen recording process, 
including starting and stopping capture, 
making it suitable for custom applications that 
require precise control.

### Context Manager: 
Designed to be used as a context manager, 
it ensures proper resource cleanup and termination, 
which is important in long-running applications.

### Example with Bluestacks: 

[![YT](https://i.ytimg.com/vi/Sw-F1sobIlY/maxresdefault.jpg)](https://www.youtube.com/watch?v=Sw-F1sobIlY)
[https://www.youtube.com/watch?v=Sw-F1sobIlY]()

```python
Capture Android device screen using ADB's screenrecord with high frame rate.

This class allows capturing the screen of an Android device using ADB's screenrecord
command with an improved frame rate. It continuously captures frames from the device
and provides them as NumPy arrays to the caller.

Args:
	adb_path (str): The path to the ADB executable.
	device_serial (str): The serial number of the target Android device.
	time_interval (int): The maximum duration, in seconds, for each screen recording session (up to a maximum of 180 seconds). After reaching this time limit, a new recording session automatically starts without causing interruptions to the user experience.
	width (int): The width of the captured screen.
	height (int): The height of the captured screen.
	bitrate (str): The bitrate for screen recording (e.g., "20M" for 20Mbps).
	use_busybox (bool): Whether to use BusyBox for base64 encoding.
	connect_to_device (bool): Whether to connect to the device using ADB.
	screenshotbuffer (int): The size of the frame buffer to store the last captured frames.
	go_idle (float): The idle time (in seconds) when no new frames are available. # higher value -> less fps, but also less CPU usage.

Attributes:
	stop_recording (bool): Control attribute to stop the screen capture.

Methods:
	stop_capture(): Stops the screen capture.

Usage:
	import cv2
	from adbnativeblitz import AdbFastScreenshots

	with AdbFastScreenshots(
		adb_path=r"C:\Android\android-sdk\platform-tools\adb.exe",
		device_serial="127.0.0.1:5555",
		time_interval=179,
		width=1600,
		height=900,
		bitrate="20M",
		use_busybox=False,
		connect_to_device=True,
		screenshotbuffer=10,
		go_idle=0,
	) as adbscreen:
		for image in adbscreen:
			cv2.imshow("CV2 WINDOW", image)
			if cv2.waitKey(1) & 0xFF == ord("q"):
				break
	cv2.destroyAllWindows()


Note:
- The `AdbFastScreenshots` class should be used in a context manager (`with` statement).
- The `stop_capture()` method can be called to stop the screen capture.
- The frames are continuously captured and provided in the form of NumPy arrays.
- The class aims to achieve a higher frame rate by avoiding slow subprocess creation
  for each screen capture session.
```