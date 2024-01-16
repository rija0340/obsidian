
## sujet 

# Find the Symmetric Difference

The mathematical term symmetric difference (`△` or `⊕`) of two sets is the set of elements which are in either of the two sets but not in both. For example, for sets `A = {1, 2, 3}` and `B = {2, 3, 4}`, `A △ B = {1, 4}`.

Symmetric difference is a binary operation, which means it operates on only two elements. So to evaluate an expression involving symmetric differences among _three_ elements (`A △ B △ C`), you must complete one operation at a time. Thus, for sets `A` and `B` above, and `C = {2, 3}`, `A △ B △ C = (A △ B) △ C = {1, 4} △ {2, 3} = {1, 2, 3, 4}`.

Create a function that takes two or more arrays and returns an array of their symmetric difference. The returned array must contain only unique values (_no duplicates_).


## code 

```php
function sym(...$arrays)
{

    $compteur = 0;
    $diff1 = [];
    $diff2 = [];
    $diffMerged = [];
    foreach ($arrays as $key => $array)
    {
        //find symetrique
        if ($key == 0)
        {
            $diffMerged = $arrays[0];
        }
        if (array_key_exists($key + 1, $arrays))
        {
            $diff1 = array_diff($diffMerged, $arrays[$key + 1]);
            $diff2 = array_diff($arrays[$key + 1], $diffMerged);
            $diffMerged = array_merge($diff1, $diff2);
        }
        else
        {
            sort($diffMerged);
            $diffMerged = array_unique($diffMerged);
            var_dump($diffMerged);
        }

    }
}

sym([1, 2, 3], [5, 2, 1, 4]);
sym([1, 2, 3], [5, 2, 1, 4]);

sym([1, 2, 3, 3], [5, 2, 1, 4]);
sym([1, 2, 3], [5, 2, 1, 4, 5]);
sym([3, 3, 3, 2, 5], [2, 1, 5, 7], [3, 4, 6, 6], [1, 2, 3], [5, 3, 9, 8], [1]);

?>
```


