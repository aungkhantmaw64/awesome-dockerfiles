# Dockerfile for ESP-IDF Development Environment

## Windows
### Requirements
- WSL2
- [USBIPD-WIN Project](https://learn.microsoft.com/en-us/windows/wsl/connect-usb)

### Getting started
- List all of the USB devices connected to Windows by running the **PowerShell** in administrator mode and entering command
```bash
usbipd list
```
- (Optional)  Register the USB device for sharing, so it can be attached to other machines (VMs). 
```bash
usbipd bind -b <busID> 
```
- Select the bus ID of the target device and run this command
```bash
usbipd attach --busid <busID> --wsl <Distro> 
```
- Build the docker image.
```bash
docker image build -f .\espidf.Dockerfile --progress tty -t espidf:latest .
```
- Start the container. Ensure `--privileged` option is included when running the container. Otherwise, the **tty\*** files will not appear in */dev* of the container.
```bash
docker container run --privileged --rm -it -v ${pwd}:/app espidf:latest bash
```
- Find out which file of the linux container is mapped to the USB device by running `dmesg` command (Normally, it is /dev/ttyUSB0).