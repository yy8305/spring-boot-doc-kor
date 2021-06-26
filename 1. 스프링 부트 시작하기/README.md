# 스프링 부트 시작하기

Spring Boot 또는 일반적인 Spring을 시작하는 경우 해당 섹션을 읽고 시작하십시오.  
기본적으로 `What`, `How`, `Why` 질문에 대한 답이 있습니다.  
여기에는 설치 지침과 함께 Spring Boot에 대한 소개 내용이 포함되어 있습니다.  
첫 번째 Spring Boot 애플리케이션을 빌드하고 몇 가지 핵심 원칙에 대해 논의해봅시다.

## 1. 스프링 부트 소개

Spring Boot를 사용하면 실행할 수 있는 독립형, 운영 등급(실제 배포 수준)의 Spring 기반 애플리케이션을 만들 수 있습니다. Spring 플랫폼과 제3자 라이브러리를 의견 수렴하여 최소한의 번거로움으로 시작할 수 있도록 합니다. 대부분의 Spring Boot 애플리케이션에는 매우 적은 Spring 설정을 하게 해줍니다.  

Spring Boot를 사용하여 `java -jar` 또는 `war 패키징`를 통해 Java 애플리케이션을 실행할 수 있습니다. 또한 "스프링 스크립트"를 실행하는 CLI(Command Line Tool)을 제공합니다.  

우리의 주요 목표는 다음과 같습니다.
- 모든 Spring 개발에 대해 근본적으로 더 빠르고 광범위하게 액세스 할 수있는 시작 환경을 제공합니다.

- 당신이 원하는 요구사항에 따라 정해진 틀에서 벗어나 기본설정에서 얼마든지 다양하고 복잡하게 만들수 있습니다.

- 대규모 프로젝트 클래스 (예 : 임베디드 서버, 보안, 메트릭, 상태 확인 및 외부 구성)에 공통적 인 다양한 비 기능적 기능을 제공합니다.

- 코드 생성(code generation)이 전혀없고 XML 설정이 필요하지 않습니다.
    > code generation ex) ruby on rails, django

---

## 2. 시스템 요구 사항

Spring Boot 2.4.5에는 Java 8이 필요 하며 Java 16까지 호환됩니다. Spring Framework 5.3.6 이상도 필요합니다.  

다음 빌드 도구에 대해 명시 적 빌드 지원이 제공됩니다.

빌드도구 | 버전
:---: | :---:
메이븐 | 3.3 이상
Gradle | 6 (6.3 이상). 5.6.x도 지원되지만 더 이상 사용되지 않는 형식입니다.

### 2.1 서블릿 컨테이너

Spring Boot는 다음과 같은 임베디드 서블릿 컨테이너를 지원합니다.

이름 | 서블릿 버전
:--: | :--:
톰캣 9.0 | 4.0
Jetty 9.4 | 3.1
Undertow 2.0 | 3.0

Servlet 3.1+ 호환 컨테이너에 Spring Boot 애플리케이션을 배포 할 수도 있습니다.

---

## 3. 스프링 부트 설지

Spring Boot는 일반적인 Java 개발 도구와 함께 사용하거나 명령 줄 도구(CLI)로 설치할 수 있습니다. 어느 쪽이든 Java SDK v1.8 이상 이 필요합니다. 시작하기 전에 다음 명령을 사용하여 현재 Java 설치를 확인해야합니다.

Java 개발을 처음 사용하거나 Spring Boot를 실행하고 싶다면 먼저 Spring Boot CLI (Command Line Interface) 를 사용해 보는 것이 좋습니다. 그렇지 않으면 일반적인 설치 지침을 읽으십시오.

### 3.1 Java 개발자를 위한 설치 지침

표준 Java 라이브러리와 동일한 방식으로 Spring Boot를 사용할 수 있습니다. 그렇게하려면 `spring-boot-*.jar` 파일을 `classpath`에 포함하십시오.  
Spring Boot에는 특별한 도구 통합이 필요하지 않으므로 어떤 IDE나 텍스트 편집기를 사용할 수 있습니다.  
또한 Spring Boot 애플리케이션에는 특별한 것이 없으므로 다른 Java 프로그램과 마찬가지로 Spring Boot 애플리케이션을 실행하고 디버그 할 수 있습니다.

Spring Boot 관련 jar들을 복사하여 사용 있지만 일반적으로 종속성 관리를 지원하는 빌드 도구(예 : Maven 또는 Gradle)를 사용하는 것이 좋습니다.

#### 3.1.1. Maven 설치

Spring Boot는 Apache Maven 3.3 이상과 호환됩니다. Maven을 아직 설치하지 않은 경우 maven.apache.org 의 지침을 따를 수 있습니다.

> 많은 운영 체제에서 Maven은 패키지 관리자로 설치할 수 있습니다. OSX 사용자는 Homebrew를 사용하는 경우   
`brew install maven`  
Ubuntu 사용자는  
`sudo apt-get install maven`    
Windows 사용자는 Chocolatey를 통해 설치 가능  
`choco install maven`

Spring Boot 종속성은 `org.springframework.boot`를 `groupId` 로 사용합니다.  
일반적으로 Maven POM 파일은 spring-boot-starter-parent프로젝트 에서 상속되며 하나 이상의 '스타터'에 대한 종속성을 선언합니다. Spring Boot는 실행 가능한 jar를 생성하기 위한 선택적 Maven 플러그인 도 제공합니다.

Spring Boot 및 Maven 시작에 대한 자세한 내용은 Maven 플러그인 참조 가이드의 시작하기 섹션에서 찾을 수 있습니다.

- spring-boot-starter-parent 의 pom.xml 예제  

    ```xml
    # 일반적인 spring-boot-stater-parent 선언방법
    <!-- Inherit defaults from Spring Boot -->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.4.5</version>
    </parent>

    # parent 없이 쓰는 경우
    <dependencyManagement>
        <dependencies>
            <dependency>
                <!-- Import dependency management from Spring Boot -->
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>2.4.5</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
    ```

#### 3.1.2. Gradle 설치

Spring Boot는 Gradle 6 (6.3 이상)과 호환됩니다. Gradle 5.6.x도 지원되지만이 지원은 더 이상 사용되지 않으며 향후 릴리스에서 제거됩니다. 아직 Gradle이 설치되어 있지 않은 경우 gradle.org 의 지침을 따를 수 있습니다.  

Spring Boot 종속성은 `org.springframework.boot`를 `group`으로 사용합니다. 일반적으로 프로젝트는 하나 이상의 '스타터'에 대한 종속성을 선언합니다. Spring Boot는 종속성 선언을 단순화하고 실행 가능한 jar를 만드는 데 사용할 수 있는 유용한 Gradle 플러그인 을 제공합니다.

> Gradle Wrapper  
Gradle Wrapper는 프로젝트를 빌드해야 할 때 Gradle을 "획득(obtaining)" 하는 좋은 방법을 제공합니다. 빌드 프로세스를 부트 스트랩하기 위해 코드와 함께 커밋하는 작은 스크립트 및 라이브러리입니다. 자세한 내용은 docs.gradle.org/current/userguide/gradle_wrapper.html 을 참조하십시오.

### 3.2. Spring Boot CLI 설치

Spring Boot CLI (Command Line Interface)는 Spring으로 빠르게 프로토 타입을 만드는 데 사용할 수있는 명령줄 도구입니다. 이를 통해 Groovy 스크립트를 실행할 수 있습니다. 즉, 많은 상용구 코드없이 익숙한 Java와 유사한 구문을 사용할 수 있습니다.  

Spring Boot로 작업하기 위해 CLI를 사용할 필요는 없지만 Spring 애플리케이션을 시작하는 가장 빠른 방법입니다.

#### 3.2.1. 수동 설치 

Spring 소프트웨어 저장소에서 Spring CLI 배포를 다운로드 할 수 있습니다.

- [spring-boot-cli-2.4.5-bin.zip](https://repo.spring.io/release/org/springframework/boot/spring-boot-cli/2.4.5/spring-boot-cli-2.4.5-bin.zip)

- [spring-boot-cli-2.4.5-bin.tar.gz](https://repo.spring.io/release/org/springframework/boot/spring-boot-cli/2.4.5/spring-boot-cli-2.4.5-bin.tar.gz)

[스냅샷](https://repo.spring.io/snapshot/org/springframework/boot/spring-boot-cli/)으로도 사용할 수 있습니다.

다운로드가 완료되면 압축을 푼 아카이브의 [INSTALL.txt](https://raw.githubusercontent.com/spring-projects/spring-boot/v2.4.5/spring-boot-project/spring-boot-cli/src/main/content/INSTALL.txt) 지침을 따르세요. 요약 하면 .zip 파일 안에 bin/ 디렉토리 안에 spring script(spring.bat for Windows) 가 있습니다. 또는 `java -jar` 와 함께 `.jar 파일`(스크립트는 classpath가 올바르게 설정되었는지 확인하는 데 도움이됩니다)을 사용할 수 있습니다.

#### 3.2.2. SDKMAN으로 설치
SDKMAN(소프트웨어 개발 키트 관리자)는 Groovy 및 Spring Boot CLI를 포함하여 다양한 바이너리 SDK의 여러 버전을 관리하는데 사용할 수 있습니다. SDKMAN을 sdkman.io 에서 받고나면 다음과 같은 명령을 사용하여 spring boot를 설치합니다.
```
$ sdk install springboot 
$ spring --version 
springboot v2.4.5
```  

CLI 용 기능을 개발하고 빌드 한 버전에 액세스하려면 다음 명령을 사용하십시오.
```
$ sdk install springboot dev /path/to/spring-boot/spring-boot-cli/target/spring-boot-cli-2.4.5-bin/spring-2.4.5/ 
$ sdk default springboot dev 
$ spring --version 
Spring CLI v2.4.5
```

앞의 지침 spring은 dev인스턴스 라는 로컬 인스턴스를 설치 합니다. 대상 빌드 위치를 가르키므로 Spring Boot를 다시 빌드 할 때마다 spring최신 상태입니다.

다음 명령을 실행하여 확인할 수 있습니다.

```
$ sdk ls springboot

================================================================================
Available Springboot Versions
================================================================================
> + dev
* 2.4.5

================================================================================
+ - local version
* - installed
> - currently in use
================================================================================
```

#### 3.2.3. OSX Homebrew 설치

Mac에서 Homebrew 를 사용하는 경우 다음 명령을 사용하여 Spring Boot CLI를 설치할 수 있습니다.

```
$ brew tap spring-io / tap 
$ brew install spring-boot
```

Homebrew는 /usr/local/bin에 spring을 설치합니다.

> formula(버전?)이 보이지 않으면 Brew 설치가 오래된 것일 수 있습니다. 이 경우 실행 brew update하고 다시 시도하십시오.

#### 3.2.4. MacPorts 설치

Mac에서 MacPorts 를 사용하는 경우 다음 명령을 사용하여 Spring Boot CLI를 설치할 수 있습니다.

```
$ sudo port install spring-boot-cli
```

#### 3.2.5 Command-line 자동완성

Spring Boot CLI에는 BASH 및 zsh 셸에 대한 Command-line 자동완성 기능을 제공하는 스크립트가 포함되어 있습니다. 당신은 어떤 쉘 이나 개인 또는 시스템 전체 bash 쉘에서 source script (spring으로 명명 된 스크립트)를 초기화에 넣어 사용할수 있습니다. Debian 시스템에서는 시스템 전체 스크립트가 /shell-completion/bash있으며 해당 디렉토리의 모든 스크립트는 새 셸이 시작될 때 실행됩니다. 예를 들어 SDKMAN!을 사용하여 설치 한 경우 스크립트를 수동으로 실행하려면 다음 명령을 사용하십시오.

```
$ . ~/.sdkman/candidates/springboot/current/shell-completion/bash/spring
$ spring <HIT TAB HERE>
  grab  help  jar  run  test  version
```
> Homebrew 또는 MacPorts를 사용하여 Spring Boot CLI를 설치하면 명령 줄 완료 스크립트가 자동으로 셸에 등록됩니다.

#### 3.2.6. Windows Scoop 설치

Windows에서 Scoop 을 사용하는 경우 다음 명령을 사용하여 Spring Boot CLI를 설치할 수 있습니다.

```
> scoop bucket add extras
> scoop install springboot
```


#### 3.2.7. 빠른 시작 Spring CLI 예제

다음 웹 애플리케이션을 사용하여 설치를 테스트 할 수 있습니다. 시작하려면 app.groovy 다음과 같이 파일을 만듭니다.

```java
@RestController
class ThisWillActuallyRun {

    @RequestMapping("/")
    String home() {
        "Hello World!"
    }

}
```

그런 다음 다음과 같이 셸에서 실행합니다.

```
$ spring run app.groovy
```

> 애플리케이션의 첫 번째 실행은 종속성이 다운로드되므로 느립니다. 후속 실행은 훨씬 더 빠릅니다.

localhost:8080 주소를 자주 사용하는 웹 브라우저에서 엽니다. 다음 출력이 표시되어야합니다.

```
Hello World!
```

### 3.3. 이전 버전의 Spring Boot에서 업그레이드

1.x Spring Boot 릴리스에서 업그레이드하는 경우 자세한 업그레이드 지침은 spring 프로젝트 위키의 "마이그레이션 가이드"를 확인하십시오. 각 릴리스의 "새롭고 주목할만한" 기능 목록은 "[릴리스 노트](https://github.com/spring-projects/spring-boot/wiki)" 에서 확인하십시오.

새 기능 릴리스로 업그레이드 할 때 일부 속성의 이름이 변경되거나 제거되었을 수 있습니다. Spring Boot는 애플리케이션의 환경을 분석하고 시작시 진단을 출력하는 방법을 제공하지만 런타임에 속성을 임시로 마이그레이션 할 수도 있습니다. 해당 기능을 사용하려면 프로젝트에 다음 종속성을 추가하십시오.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-properties-migrator</artifactId>
    <scope>runtime</scope>
</dependency>
```
> 마이그레이션이 완료되면 프로젝트의 종속성에서이 모듈을 제거해야합니다.

기존 CLI 설치를 업그레이드하려면 적절한 패키지 관리자 명령(예 : brew upgrade)을 사용하십시오. CLI를 수동으로 설치 한 경우 표준 지침을 따르고 PATH환경 변수를 업데이트하여 이전 참조를 제거하십시오.

## 4. 첫 번째 스프링 부트 애플리케이션 개발

이 섹션에서는 “Hello World!” 프로그램을 개발하는 방법에 대해 설명합니다. Spring Boot의 주요 기능 중 일부를 강조하는 웹 애플리케이션입니다. 대부분의 IDE에서 지원하므로 Maven을 사용하여 해당 프로젝트를 빌드합니다.

> [spring.io](https://spring.io) 에서는 "Getting stated"를 포함한 많은 가이드에서 Spring boot를 사용합니다. 특정 문제를 해결해야하는 경우 먼저 확인하십시오.

> start.spring.io 로 이동하여 종속성 검색기에서 "Web" Starter를 선택하여 아래 단계를 단축 할 수 있습니다. 이렇게하면 새 프로젝트 구조가 생성되어 즉시 코딩 을 시작할 수 있습니다. 자세한 내용은 Spring Initializr 문서 를 확인하십시오.

시작하기 전에 터미널을 열고 다음 명령을 실행하여 유효한 Java 및 Maven 버전이 설치되어 있는지 확인하십시오.

```
$ java -version
java version "1.8.0_102"
Java(TM) SE Runtime Environment (build 1.8.0_102-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.102-b14, mixed mode)
```

```
$ mvn -v
Apache Maven 3.5.4 (1edded0938998edf8bf061f1ceb3cfdeccf443fe; 2018-06-17T14:33:14-04:00)
Maven home: /usr/local/Cellar/maven/3.3.9/libexec
Java version: 1.8.0_102, vendor: Oracle Corporation
```

> 이 샘플은 자체 디렉토리에 만들어야합니다. 후속 지침에서는 적합한 디렉토리를 작성했으며 현재 디렉토리라고 가정합니다.

### 4.1. POM 생성
먼저 Maven pom.xml 파일을 만들어야 합니다.   
pom.xml은 프로젝트를 빌드하는 데 사용되는 방법이다. 좋아하는 텍스트 편집기를 열고 다음을 추가하십시오.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>myproject</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.4.5</version>
    </parent>

    <description/>
    <developers>
        <developer/>
    </developers>
    <licenses>
        <license/>
    </licenses>
    <scm>
        <url/>
    </scm>
    <url/>

    <!-- Additional lines to be added here... -->

</project>
```

이전 목록은 작동하는 빌드를 제공해야합니다.   
`mvn package` 명령어를 실행하여 테스트 할 수 있습니다. ("jar will be empty - no content was marked for inclusion!" 지금은 해당 경고를 무시할 수 있습니다.)

> 이 시점에서 프로젝트를 IDE로 가져올 수 있습니다. (대부분의 최신 Java IDE에는 Maven에 대한 기본 지원이 포함됩니다.) 간단하게 하기 위해 이 예제에서는 일반 텍스트 편집기를 계속 사용합니다.

### 4.2. 클래스 경로 종속성 추가

Spring Boot는 클래스 경로에 jar를 추가 할 수있는 여러 "스타터"를 제공합니다. smoke 테스트에 대한 우리의 응용 프로그램은 POM 섹션 spring-boot-starter-parent에서 사용합니다 parent. 는 spring-boot-starter-parent유용 메이븐 기본값을 제공하는 특별 선발한다. 또한 "축복 된" 종속성에 대한 태그를 dependency-management 생략 할 수 있는 섹션 도 제공합니다 version.



# Reference
- https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started.html#getting-started