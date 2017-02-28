# packages-test
Laravel 패키지 제작 Demo


Composer 를 이용한 패키지 생성
conposer init 실행

> $ composer init
```bash


  Welcome to the Composer config generator


This command will guide you through creating your composer.json config.

Package name (<vendor>/<name>) [anyman/test-package]:
Description []:
Author [김광철 <anyman@afreecatv.com>, n to skip]:
Minimum Stability []:
Package Type (e.g. library, project, metapackage, composer-plugin) []:
License []:

Define your dependencies.

Would you like to define your dependencies (require) interactively [yes]?
Search for a package:
Would you like to define your dev dependencies (require-dev) interactively [yes]?
Search for a package:

{
    "name": "anyman/test-package",
    "authors": [
        {
            "name": "김광철",
            "email": "anyman@afreecatv.com"
        }
    ],
    "require": {}
}

Do you confirm generation [yes]? yes
```

src 폴더생성
> mkdir src


composer.json 파일에 패키지 namespace 를 지정해준다.
```json
{
    "autoload": {
        "psr-4": {
            "Lomi525\\Packagestest\\": "src/"
        }
    }
}

```
* namespcae명을 정하고 경로를 src로 지정합니다.
* src 폴더 밑은 Lomi525\Packagetest 가 됩니다.
* namespace에 첫글자는 대문자로 지정합니다.



-----------------
# 라라벨로 클래스 제작


라라벨 패키지 제작을 위해서는  라라벨클래스를 해야하므로 추가패키지를 설치한다
composer.json에 수정
```json
{
    "require": {
        "php": ">=5.3.0",
        "illuminate/support": "^4.0|^5.0"
    },
}
```
* composer update
* vender에 illuminate/support 패키지가 설치됩니다.



### ServiceProvier 제작
[ServiceProvier](https://laravel.kr/docs/5.0/providers) : 라라벨에서 서비스될때 Bootstrap을 통해 로드됩니다.

예) PackageServiceProvider
```php
<?php
/**
 * Created by PhpStorm.
 * User: anyman
 * Date: 2017-02-24
 * Time: 오후 6:33
 */

namespace Lomi525\Packagestest;


use Illuminate\Support\ServiceProvider;

class PackageServiceProvider extends ServiceProvider
{
    /**
     * Indicates if loading of the provider is deferred.
     *
     * @var bool
     */
    protected $defer = false;


    public function boot()
    {
    }

    public function register()
    {
    }

}
```
* Illuminate\Support\ServiceProvider를 상속 받는다
* boot() , registor() 의 메소드을 만들어 줍니다.
* 패키지 제작을 위한 ServiceProvider 내용은 Documents 참고바랍니다. ([링크](https://laravel.kr/docs/5.4/packages))




-----------------
# 내 패키지를  PHP Package Repository 에 올리기

### GitHup (저장소)에 내소스 올리기

```bash
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/lomi525/test.git
git push -u origin master
```


### Package Repository 등록하기




##### 자동 업데이트 설정 #####
github 에 패키지의 새 버전을 릴리스했다고 가정해 보자.
릴리스마다 Packagist 에도 올려야 한다면 매우 번거로울 것이다. github 의 hook 을 설정하면 새 버전 릴리스시 자동으로 Packagist 에 반영되도록 할 수 있다.

1) https://packagist.org/profile/ 에 들어간 후에 Your API Token 에 있는 토큰을 복사한다.
![API_TOKEN](https://raw.githubusercontent.com/lomi525/packages-test/master/images/1.png)

2) github 에 로그인 한후에 프로젝트로 들어간다.
3) 우측의 프로젝트 Settings 버튼을 클릭한다. 상단의 Settings 버튼은 계정 설정이므로 프로젝트 설정으로 들어가야 한다.
![API_TOKEN](https://raw.githubusercontent.com/lomi525/packages-test/master/images/3.png)
4) Integrations & Services  를 클릭한다.
5) Add Service 를 클릭한 후에 Packagist 를 찾아서 등록한다.
![API_TOKEN](https://raw.githubusercontent.com/lomi525/packages-test/master/images/5.png)


6) User 항목에 id를 입력하고 Token 항목에 1번에서 복사한 API token을 붙여 넣는다.
![API_TOKEN](https://raw.githubusercontent.com/lomi525/packages-test/master/images/6.png)
7)Add Service 를 클릭하여 저장한다.



-----------------
# Private 저장소를 사용하기위한 composer.json 설정
```json
{
    "repositories": [
        {
            "type": "vcs",
            "url":  "https://test.gitlab.com/test.git"
        }
    ]
}
```
* 비밀번호가 있는 경우  ~/.composer/auth.json 에 저장 된다


