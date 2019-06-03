FROM njunge/openjdk-gradle:8-jdk-5-gradle
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
	
RUN mkdir ~/.android && echo '### User Sources for Android SDK Manager' > ~/.android/repositories.cfg
RUN yes | android-sdk-linux/tools/bin/sdkmanager --licenses && yes | android-sdk-linux/tools/bin/sdkmanager --update

# Update SDK manager and install system image, platform and build tools
RUN android-sdk-linux/tools/bin/sdkmanager \
  "tools" \
  "platform-tools" \
  "emulator"
  
RUN android-sdk-linux/tools/bin/sdkmanager \
  "build-tools;${ANDROID_BUILD_TOOLS}" \
  "extras;google;m2repository" \
  "extras;android;m2repository"

RUN android-sdk-linux/tools/bin/sdkmanager "platforms;android-24" \
	"platforms;android-26" \
	"platforms;android-28"

RUN chmod 777 -R android-sdk-linux
