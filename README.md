# packages-test
Laravel 패키지 제작 Demo


Composer 를 이용한 패키지 생성
conposer init 실행

```bash
$ composer init

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





