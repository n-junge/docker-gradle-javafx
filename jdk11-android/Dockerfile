FROM njunge/openjdk-gradle:11-jdk
WORKDIR /

ENV ANDROID_HOME=$PWD/android-sdk-linux
ENV PATH=$PATH:$PWD/android-sdk-linux/platform-tools/

ENV ANDROID_COMPILE_SDK="28"
ENV ANDROID_BUILD_TOOLS="28.0.3"
ENV ANDROID_SDK_TOOLS="26.1.1"

USER root
RUN apt-get --quiet update --yes \
	&& apt-get --quiet install --yes lib32stdc++6 lib32z1 \
	&& wget --quiet --output-document=android-sdk.zip https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip \
	&& unzip -q android-sdk.zip -d android-sdk-linux
RUN mkdir android-sdk-linux/licenses \
	&& printf "8933bad161af4178b1185d1a37fbf41ea5269c55\nd56f5187479451eabf01fb78af6dfcb131a6481e" > android-sdk-linux/licenses/android-sdk-license \
	&& printf "84831b9409646a918e30573bab4c9c91346d8abd" > android-sdk-linux/licenses/android-sdk-preview-license
	
RUN mkdir ~/.android && echo '### User Sources for Android SDK Manager' > ~/.android/repositories.cfg
#RUN android-sdk-linux/tools/bin/sdkmanager --update > update.log \ 
#	&& android-sdk-linux/tools/bin/sdkmanager "platforms;android-${ANDROID_COMPILE_SDK}" "build-tools;${ANDROID_BUILD_TOOLS}" "extras;google;m2repository" "extras;android;m2repository" > installPlatform.log

RUN chmod 777 -R android-sdk-linux
