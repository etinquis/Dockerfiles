FROM amd64/alpine:latest

RUN apk update && apk upgrade

ARG ANDROID_NDK=r24
ADD https://dl.google.com/android/repository/android-ndk-$ANDROID_NDK-linux.zip android-ndk.zip

RUN unzip android-ndk.zip -d /
ENV ANDROID_NDK /android-ndk-$ANDROID_NDK
ENV ANDROID_NDK_ROOT $ANDROID_NDK

ARG CMAKE_VERSION=3.23.1-r0
RUN apk add cmake=$CMAKE_VERSION

RUN apk add bash build-base gcompat

ENV PATH=$ANDROID_NDK/toolchains/llvm/prebuilt/linux-x86_64/bin:$ANDROID_NDK/prebuilt/linux-x86_64/bin:$PATH