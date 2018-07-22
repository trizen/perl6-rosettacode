[1]: https://rosettacode.org/wiki/Generator/Exponential

# [Generator/Exponential][1]

As with Haskell, generators are disguised as lazy lists in Perl&#160;6.

```perl
sub powers($m) { $m XR** 0..* }
 
my @squares = powers(2);
my @cubes   = powers(3);
 
sub infix:<with-out> (@orig,@veto) {
    gather for @veto -> $veto {
        take @orig.shift while @orig[0] before $veto;
        @orig.shift if @orig[0] eqv $veto;
    }
}
 
say (@squares with-out @cubes)[20 ..^ 20+10].join(', ');
```

#### Output:
```
529, 576, 625, 676, 784, 841, 900, 961, 1024, 1089
```