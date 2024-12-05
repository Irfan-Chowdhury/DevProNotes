<div align='center'>

# Binary Search Algorithm

</div>

<br><br>


```php
<?php 

function binarySearch($arr, $target) {
    $low = 0;
    $high = count($arr) - 1;

    while ($low <= $high) {
        $mid = floor(($low + $high) / 2);

        // Check if the mid element is the target
        if ($arr[$mid] == $target) {
            return "Target $target found at index $mid";
        }

        // If target is smaller, search the left half
        // if ($arr[$mid] > $target) {
        //     $high = $mid - 1;
        // } else {  // If target is larger, search the right half
        //     $low = $mid + 1;
        // }

        if ($arr[$mid] < $target) {
            $low = $mid + 1;
        } else {  // If target is larger, search the left half
            $high = $mid - 1;
        }
    }
    return "Target $target not found in the array.";
}

// Test the function
$array = [3, 6, 8, 12, 14, 17, 25, 29, 31, 36, 42, 47, 53, 55, 62];
$target = 42;
echo binarySearch($array, $target);
echo "\n";
```

Result 
```bash
Target 42 found at index 10
```