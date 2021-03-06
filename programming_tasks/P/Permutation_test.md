[1]: https://rosettacode.org/wiki/Permutation_test

# [Permutation test][1]

```perl
sub stats ( @test, @all ) {
    (([+] @test) / +@test ) - ([+] flat @all, (@test X* -1)) / (@all - @test)
}


my int @treated = <85 88 75 66 25 29 83 39 97>;
my int @control = <68 41 10 49 16 65 32 92 28 98>;
my int @all = flat @treated, @control;

my $base = stats( @treated, @all );

my @trials = 0, 0, 0;

@trials[ 1 + ( stats( $_, @all ) <=> $base ) ]++ for @all.combinations(+@treated);

say 'Counts: <, =, > ', @trials;
say 'Less than    : %', 100 * @trials[0] / [+] @trials;
say 'Equal to     : %', 100 * @trials[1] / [+] @trials;
say 'Greater than : %', 100 * @trials[2] / [+] @trials;
say 'Less or Equal: %', 100 * ( [+] @trials[0,1] ) / [+] @trials;
```

#### Output:
```
Counts: <, =, > 80238 313 11827
Less than    : %86.858343
Equal to     : %0.338825
Greater than : %12.802832
Less or Equal: %87.197168
```
