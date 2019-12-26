바이앱스 라라벨 프로젝트 코딩 규약
==================================

* 참고 사이트
1. [Laravel 공식 사이트 Coding Style](https://laravel.com/docs/5.8/contributions#coding-style)  
2. [쉽게 배우는 라라벨 5 프로그래밍 - PHP 5 의 특징 - PHP 표준 권고(PSR)](https://www.lesstif.com/pages/viewpage.action?pageId=24445325)
3. [PHP Standards Recommendations](https://www.php-fig.org/psr/)
4. [PSR-1 Basic Coding Standard 한글 번역](https://ujuc.github.io/2018/11/17/psr-1:_basic_coding_standard/)
5. [PSR-2 Coding Style Guide 한글 번역](https://ujuc.github.io/2019/02/05/psr-2:_coding_style_guide/)
6. [Laravel Best Practice](https://github.com/alexeymezenin/laravel-best-practices)
7. [Laravel Best Practice 한글 번역](https://github.com/xotrs/laravel-best-practices)


---

라라벨은 PSR-2 코딩 표준과 PSR-4 오토로딩 표준을 따릅니다. 따라서 본 문서는 이를 기반으로 작성합니다.

문서 내에서 자주 쓰일 용어들은 원어보다는 (가급적) 외래어 표기법에 따른 한글로 표기합니다.
의미가 분명하지 않을 경우 괄호로 설명이나 원어를 기재합니다.

---

## 1. PSR 코딩 표준에 따른 기본 사항

### 1.1 파일

- 파일은 BOM(<sup>Byte Order Mark</sup> 문서 맨 앞에 보이지않는 특정 바이트를 넣어 인코딩방식을 알아내는 방법.[참조](http://madalla.kr/bbs/board.php?bo_table=data_etc&wr_id=50&sca=php&page=1))없는 UTF-8 인코딩을 사용한다.  
  + Windows의 메모장, Dreamweaver, Editor Plus 등에서 파일 생성시 인코딩 방식이 UTF-8+가 아닌 UTF-8인지 확인
- PHP만 포함된 파일에서는 닫는 태그(?>)는 사용하지 않는다.  
- 파일은 반드시 하나의 빈 줄로 끝나야 한다.
- namespace, class는 오토로딩 표준을 따른다.  

### 1.2 라인과 공백

- 들여쓰기는 탭이 아닌 공백 4칸을 사용한다.
- 줄 길이는 80자 이하를 권장한다.
- if, elseif 같은 제어 구문은 제어문 뒤에 공백 1개를 두고 괄호 안에 조건문을 기술한다.
- 함수나 메소드를 호출할 때는 함수명, 메소드명과 괄호 사이에는 공백을 쓰지 않는다.

```php
                // 함수명, 메소드명과 괄호 사이에는 공백 없음
public function sampleFunction($a, $b = null)
{
// 들여쓰기는 공백 4칸

    // 제어구문 뒤에 공백 1칸 쓰고 괄호
    if ($a === $b) {
        bar();
    }
}
```

- 인수 목록은 쉼표 뒤에 공백이 와야한다.
- default 값을 가지는 인수는 인수목록의 마지막에 위치한다.

```php
<?php
namespace Vendor\Package;

class ClassName
{
               // 인수 목록은 쉼표 뒤에 공백  // default 값을 가지는 인수는 목록의 마지막에.
    public function foo($arg1, &$arg2, $arg3 = [])
    {
    }
}
```

### 1.3 괄호

- class 구문의 여는 괄호는 다음 줄에 쓰고, 닫는 괄호는 본문 다음 줄에 쓴다.  
- 메소드 구문의 여는 괄호는 다음 줄에 쓰고, 닫는 괄호는 본문 맨 끝에서 다음 줄에 쓴다.  
- 제어구문의 여는 괄호는 제어문과 같은 줄에 위치하고, 닫는 괄호는 본문 다음에 위치한다.

```php
<?php
namespace Vendor\Package;

class ClassName
{   // class 구문의 여는 괄호는 class 다음 줄에

    public function foo($arg1, &$arg2, $arg3 = [])
    {  // 메소드 구문의 여는 괄호는 다음 줄에
        if ($a === $b) {    // 여는 괄호는 제어문과 같은 줄에 위치
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } // 닫는 괄호는 본문 다음 줄에 위치
    } // 메소드 구문의 닫는 괄호는 본문 맨 끝에서 다음 줄에


} //class 구문의 닫는 괄호는 본문 다음 줄에
```

### 1.4 예약어와 true/false/null

- global, const, var 등의 [예약어](http://php.net/manual/en/reserved.keywords.php)와 true,false,null등은 반드시 소문자로 작성한다.
- public, private, protected 와 같은 가시성 키워드는 모든 property와 method에서 반드시 선언되어야 한다.
- abtract, final은 가시성 키워드 이전에 선언되어야 한다.
- static은 반드시 가시성 키워드 뒤에 선언되어야 한다.

```php
abstract class ClassName
{
    // 가시성 키워드는 모든 property와 method에서 반드시 선언
    protected static $foo;

    // abstract, final은 가시성 키워드 이전에 선언
    abstract protected function zim();

    // static은 가시성 키워드 뒤에 선언
    final public static function bar()
    {
       const SOMETHING = true;  // 예약어와 true/false/null은 반드시 소문자로
    }
}
```

### 1.5 namespace와 class

- namespace 선언 다음에는 빈 줄이 하나 있어야 한다.
- use 선언 다음에는 빈 줄이 하나 있어야 한다.

```php
namesapce Vender\Package;

use FooClass;
use BarClass as Bar;
use OhterVender\OtherPackage\BazClass;

// ... additinal PHP code ...
```

- class 이름은 반드시 첫 글자를 대문자로 한다.  
- class 내 상수는 모두 대문자로 하고 밑줄을 구분 기호로 해서 선언한다.  
- class 내 메소드 이름은 camelCase를 사용한다.
- 메소드, property의 이름을 밑줄로 시작하면 안된다.


## 2. Laravel Best Practice 문서 참고 사항  

[Laravel best practice 문서 중 네이밍 규칙 부분을 발췌](https://github.com/xotrs/laravel-best-practices#라라벨-네이밍-규칙을-따릅니다)

| 항목                             | 방식                         | 좋은 예                               | 나쁜 예                                                  |
|----------------------------------|------------------------------|---------------------------------------|----------------------------------------------------------|
| Controller                       | 단수형                       | ArticleController                     | ~~ArticlesController~~                                   |
| Route                            | 복수형                       | articles/1                            | ~~article/1~~                                            |
| Named route                      | 온점 표기와 snake_case       | users.show_active                     | ~~users.show-active, show-active-users~~                 |
| Model                            | 단수형                       | User                                  | ~~Users~~                                                |
| hasOne or belongsTo relationship | 단수형                       | articleComment                        | ~~articleComments~~   ~~article_comment~~                |
| All other relationships          | 복수형                       | articleComments                       | ~~articleComment~~   ~~article_comments~~                |
| Table                            | 복수형                       | article_comments                      | ~~article_comment~~   ~~articleComments~~                |
| Pivot table                      | 알파벳 순서로 단수형 모델명  | article_user                          | ~~user_article~~   ~~articles_users~~                    |
| Table column                     | 모델명 없이 snake_case       | meta_title                            | ~~MetaTitle~~   ~~article_meta_title~~                   |
| Model property                   | snake_case                   | $model->created_at                    | ~~$model->createdAt~~                                    |
| Foreign key                      | 뒤에 id를 붙인 단수형 모델명 | article_id                            | ~~ArticleId~~   ~~id_article~~   ~~articles_id~~         |
| Method                           | camelCase                    | getAll                                | ~~get_all~~                                              |
| Method in resource controller    | * 별도 테이블 참조           |                                       |                                                          |
| Method in test class             | camelCase                    | testGuestCannotSeeArticle             | ~~test_guest_cannot_see_article~~                        |
| Variable                         | camelCase                    | $articlesWithAuthor                   | ~~$articles_with_author~~                                |
| Collection                       | 설명식으로, 복수형           | $activeUsers = User::active()->get()  | ~~$active, $data~~                                       |
| Object                           | 설명식으로, 단수형           | $activeUser = User::active()->first() | ~~$users, $obj~~                                         |
| Config and language files index  | snake_case                   | articles_enabled                      | ~~ArticlesEnabled; articles-enabled~~                    |
| View                             | snake_case                   | show_filtered.blade.php               | ~~showFiltered.blade.php~~   ~~show-filtered.blade.php~~ |
| Config                           | snake_case                   | google_calendar.php                   | ~~googleCalendar.php~~   ~~google-calendar.php~~         |
| Contract (interface)             | 형용사형 또는 명사형         | Authenticatable                       | ~~AuthenticationInterface~~ ~~IAuthentication~~          |
| Trait                            | 형용사형                     | Notifiable                            | ~~NotificationTrait~~                                    |

- Laravel Best Practice에는 없고 별도로 추가

| 항목                             | 방식                         | 좋은 예                               | 나쁜 예                                                  |
|----------------------------------|------------------------------|---------------------------------------|----------------------------------------------------------|
| Factory                          | StudlyCase, 단수형           | PostFactory                           |                                                          |
| Seeder                           | 대상 테이블이름 뒤에 Seeder  | UsersTableSeeder                      |                                                          |

- resource controller 테이블

| Verb      | URI                  | Action  | Route Name     |
|-----------|----------------------|---------|----------------|
| GET       | /photos              | index   | photos.index   |
| GET       | /photos/create       | create  | photos.create  |
| POST      | /photos              | store   | photos.store   |
| GET       | /photos/{photo}      | show    | photos.show    |
| GET       | /photos/{photo}/edit | edit    | photos.edit    |
| PUT/PATCH | /photos/{photo}      | update  | photos.update  |
| DELETE    | /photos/{photo}      | destroy | photos.destroy |
