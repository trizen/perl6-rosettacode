[1]: https://rosettacode.org/wiki/Stern-Brocot_sequence

# [Stern-Brocot sequence][1]

```raku
constant @Stern-Brocot = 1, 1, {
    |(@_[$_ - 1] + @_[$_], @_[$_]) given ++$
} ... *;
 
say @Stern-Brocot[^15];
 
for (flat 1..10, 100) -> $ix {
    say "first occurrence of $ix is at index : ", 1 + @Stern-Brocot.first($ix, :k);
}
 
say so 1 == all map ^1000: { [gcd] @Stern-Brocot[$_, $_ + 1] }
```

#### Output:
```
1 1 2 1 3 2 3 1 4 3 5 2 5 3 4
first occurrence of 1 is at index : 1
first occurrence of 2 is at index : 3
first occurrence of 3 is at index : 5
first occurrence of 4 is at index : 9
first occurrence of 5 is at index : 11
first occurrence of 6 is at index : 33
first occurrence of 7 is at index : 19
first occurrence of 8 is at index : 21
first occurrence of 9 is at index : 35
first occurrence of 10 is at index : 39
first occurrence of 100 is at index : 1179
True
```