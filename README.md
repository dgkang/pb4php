# pb4php
fork from https://code.google.com/archive/p/pb4php

# 说明
简单，一个proto文件，就生成一个PHP文件，并且不依赖于protoc，也不使用任何PHP的protobuf插件。  
支持protoV2  

# 生成PHP文件
cd example  
php protoc.php test.proto  

# 例子
```PHP
<?phprequire_once('parser/pb_parser.php');
$test = new PBParser();
$test->parse('./test.proto');

require_once('message/pb_message.php');
require_once('pb_proto_test.php');
$string = file_get_contents('./example/test.pb');

$book = new AddressBook();
$person = $book->add_person();
$person->set_name('Kordulla');
$person->set_surname('Nikolai');

$phone_number = $person->add_phone();
$phone_number->set_number('49');
$phone_number->set_type(Person_PhoneType::WORK);

$phone_number = $person->add_phone();
$phone_number->set_number('171');
$phone_number->set_type(Person_PhoneType::MOBILE);

// serialize$string = $book->SerializeToString();
//echo $string;// write it to disk
file_put_contents('adressbook.pb', $string);
$string = file_get_contents('./adressbook.pb');
// Just read it$book = new AddressBook();
$book->parseFromString($string);

var_dump($book->person_size());
$person = $book->person(0);
var_dump($person->name());
var_dump($person->surname());
var_dump($person->phone(0)->number());
var_dump($person->phone(0)->type());
var_dump($person->phone(1)->number());
var_dump($person->phone(1)->type());
?>
```


