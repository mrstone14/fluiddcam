FROM debian:bullseye

ENV DEBIAN_FRONTEND noninteractive

RUN apt update && apt install -y cmake build-essential curl git

#RUN echo "deb http://archive.raspberrypi.org/debian/ bullseye main" > /etc/apt/sources.list.d/raspi.list
RUN printf "deb http://deb.debian.org/debian bullseye main contrib non-free\ndeb http://security.debian.org/debian-security bullseye-security main contrib non-free\ndeb http://deb.debian.org/debian bullseye-updates main contrib non-free" > /etc/apt/sources.list
#RUN curl "https://archive.raspberrypi.org/debian/raspberrypi.gpg.key" | apt-key add -

RUN apt update && apt full-upgrade -y

#RUN apt list -a raspberrypi-kernel
#RUN apt policy raspberrypi-kernel-headers
#RUN apt install raspberrypi-kernel-headers
#RUN apt install raspberrypi-kernel

RUN apt update && apt install -y libcamera-dev libjpeg-dev libgphoto2-dev

RUN git clone https://github.com/ArduCAM/mjpg-streamer.git /src
WORKDIR /src/mjpg-streamer-experimental

RUN sed -i "/input_libcamera/p;/input_/d;/output_http/p;/output_/d" CMakeLists.txt
RUN make && make install

COPY entrypoint.sh entrypoint.sh
ENV INPUT_FLAGS "-r 1920x1080 -f 60"
ENV OUTPUT_FLAGS "-w ./www"
ENTRYPOINT ["./entrypoint.sh"]
