# OpenJDK 

- 설치 파일 다운로드 : https://github.com/AdoptOpenJDK/openjdk8-upstream-binaries/releases

  * 안정성을 위해 GA 버전을 다운로드 받는다

  * [OpenJDK8U-jdk_x64_linux_8u342b07.tar.gz](https://github.com/AdoptOpenJDK/openjdk8-upstream-binaries/releases/download/jdk8u342-b07/OpenJDK8U-jdk_x64_linux_8u342b07.tar.gz)

* OpenJDK와 OracleJDK 간의 성능 차이는 없음, Oracle JDK에는 몇가지 보완 툴이 있으며, 그 부분만 유료

* 설치파일을 서버로 이동(FTP)

* 설치 디렉토리 만들기

  ```shell
  mkdir /usr/lib/java
  ```

* 압축 해제 및 설치 디렉토리로 이동

  ```shell
  [root@kcwbigsv03t upload_files]# tar -xvzf OpenJDK8U-jdk_x64_linux_8u342b07.tar.gz
  [root@kcwbigsv03t upload_files]# mv openjdk-8u342-b07 /usr/lib/java/
  [root@kcwbigsv03t upload_files]# ll /usr/lib/java/
  합계 0
  drwxrwxr-x. 9 501 501 188  7월 16  2022 openjdk-8u342-b07
  ```

* 환경변수 설정 (/etc/profile)

  ```shell
  # vi /etc/profile
  export JAVA_HOME=/usr/lib/java/openjdk-8u342-b07
  export PATH=$JAVA_HOME/bin:$PATH
  export CLASSPATH=$CLASSPATH=$JAVA_HOME/jre/lib/ext:$JAVA_HOME/lib/tools.jar
  
  # source /etc/profile
  ```

* 설치 확인

  ```shell
  [root@kcwbigsv03t upload_files]# java -version
  openjdk version "1.8.0_342"
  OpenJDK Runtime Environment (build 1.8.0_342-b07)
  OpenJDK 64-Bit Server VM (build 25.342-b07, mixed mode)
  ```

  



