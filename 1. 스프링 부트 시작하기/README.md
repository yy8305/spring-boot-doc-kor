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
    > code generation -> ruby on rails의 skeleton 같은 기술

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

    ```
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

### 3.1.2. Gradle 설치

Spring Boot는 Gradle 6 (6.3 이상)과 호환됩니다. Gradle 5.6.x도 지원되지만이 지원은 더 이상 사용되지 않으며 향후 릴리스에서 제거됩니다. 아직 Gradle이 설치되어 있지 않은 경우 gradle.org 의 지침을 따를 수 있습니다.  

Spring Boot 종속성은 `org.springframework.boot`를 `group`으로 사용합니다. 일반적으로 프로젝트는 하나 이상의 '스타터'에 대한 종속성을 선언합니다. Spring Boot는 종속성 선언을 단순화하고 실행 가능한 jar를 만드는 데 사용할 수 있는 유용한 Gradle 플러그인 을 제공합니다.

> Gradle Wrapper  
Gradle Wrapper는 프로젝트를 빌드해야 할 때 Gradle을 "획득(obtaining)" 하는 좋은 방법을 제공합니다. 빌드 프로세스를 부트 스트랩하기 위해 코드와 함께 커밋하는 작은 스크립트 및 라이브러리입니다. 자세한 내용은 docs.gradle.org/current/userguide/gradle_wrapper.html 을 참조하십시오.

## 3.2. Spring Boot CLI 설치

Spring Boot CLI (Command Line Interface)는 Spring으로 빠르게 프로토 타입을 만드는 데 사용할 수있는 명령줄 도구입니다. 이를 통해 Groovy 스크립트를 실행할 수 있습니다. 즉, 많은 상용구 코드없이 익숙한 Java와 유사한 구문을 사용할 수 있습니다.  

Spring Boot로 작업하기 위해 CLI를 사용할 필요는 없지만 Spring 애플리케이션을 시작하는 가장 빠른 방법입니다.

### 3.2.1. 수동 설치 

Spring 소프트웨어 저장소에서 Spring CLI 배포를 다운로드 할 수 있습니다.

- [spring-boot-cli-2.4.5-bin.zip](https://repo.spring.io/release/org/springframework/boot/spring-boot-cli/2.4.5/spring-boot-cli-2.4.5-bin.zip)

- [spring-boot-cli-2.4.5-bin.tar.gz](https://repo.spring.io/release/org/springframework/boot/spring-boot-cli/2.4.5/spring-boot-cli-2.4.5-bin.tar.gz)

[스냅샷](https://repo.spring.io/snapshot/org/springframework/boot/spring-boot-cli/)으로도 사용할 수 있습니다.

다운로드가 완료되면 압축을 푼 아카이브의 [INSTALL.txt](https://raw.githubusercontent.com/spring-projects/spring-boot/v2.4.5/spring-boot-project/spring-boot-cli/src/main/content/INSTALL.txt) 지침을 따릅니다. 요약 하면 파일 의 디렉토리에 spring스크립트 (spring.bat Windows용) bin/가 .zip 있습니다. 또는 파일 java -jar과 함께 사용할 수 있습니다. jar(스크립트는 클래스 경로가 올바르게 설정되었는지 확인하는 데 도움이됩니다).

# Reference
- https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started.html#getting-started