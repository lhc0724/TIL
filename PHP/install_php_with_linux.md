# 리눅스 환경에서 PHP 시작하기 

> 서술할 환경은 다음과 같습니다.  
> Linux - Debian  
> Apache 2.x  
> MySQL  
> Laravel 8.x Framework  
> PHP 8.x  

## PHP8 소개
기존 php5.x 혹은 php7.x에 비해 미래지향적인 기능들이 대거 도입되었으며,    
새로운 기능을 제외하고도 __JIT__ 의 도입으로 속도면에서도 최근 핫한 타 언어들과도 견줄 수 있게 되었다.  

- ### JIT?
    Just In Time의 약자로 런타임에 코드의 일부를 기계어로 컴파일하여 인터프리터임에도 미리  
    코드가 캐시되어 빠르게 불러와 동작하는 최적화 기술이다.

    코드의 실행 빈도에 따라, warm/hot으로 나누어 hot 파트를 기계어로 컴파일 되어 즉석하여 사용 할 수 있다.

## PHP8.x 설치하기
1. 먼저 OS의 시스템과 패키지들을 업데이트 해준다.
    ```shell
    sudo apt update && sudo apt upgrade -y
    ``` 

2. PHP8 Sury 저장소 가져오기  
해외 자료에 따르면 Ubuntu, CentOS, Fedora, Debian 등의 다른 저장소도 있는 모양이지만,   
여기서는 Sury Reository를 이용하였다.  
저장소를 추가 하기 전 __GPG Key__ 를 다운로드 한다.  
    ```shell
    sudo wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
    ```
    GPG키를 다운로드 후 Sury 저장소를 추가한다.
    ```shell
    sudo sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
    ```
    변경 사항을 반영하기 위해 update/upgrade 실행.
    ```shell
    sudo apt update
    sudo apt upgrade
    ``` 
    
