[1]: https://rosettacode.org/wiki/Polynomial_long_division

# [Polynomial long division][1]

```perl
sub poly_long_div ( @n is copy, @d ) {
    return [0], |@n if +@n < +@d;
 
    my @q = gather while +@n >= +@d {
        @n = @n Z- flat ( ( @d X* take ( @n[0] / @d[0] ) ), 0 xx * );
        @n.shift;
    }
 
    return $(@q), $(@n);
}
 
sub xP ( $power ) { $power>1 ?? "x^$power" !! $power==1 ?? 'x' !! '' }
sub poly_print ( @c ) { join ' + ', @c.kv.map: { $^v ~ xP( @c.end - $^k ) } }
 
my @polys = [ [     1, -12, 0, -42 ], [    1, -3 ] ],
            [ [     1, -12, 0, -42 ], [ 1, 1, -3 ] ],
            [ [          1, 3,   2 ], [    1,  1 ] ],
            [ [ 1, -4,   6, 5,   3 ], [ 1, 2,  1 ] ];
 
say '<math>\begin{array}{rr}';
for @polys -> [ @a, @b ] {
    printf Q"%s , & %s \\\\\n", poly_long_div( @a, @b ).map: { poly_print($_) };
}
say '\end{array}</math>';
```


Output:



![image](https://rosettacode.org/mw/index.php?title=Special:MathShowImage&hash=0b87cf3373b9b349c7550caf5964ad1c&mode=mathml)