[1]: https://rosettacode.org/wiki/Draw_a_sphere

# [Draw a sphere][1]

The C code is modified to output a .pgm file.

```perl
my $x = my $y = 255;
$x +|= 1; # must be odd
 
my @light = normalize([ 3, 2, -5 ]);
 
my $depth = 255;
 
sub MAIN ($outfile = 'sphere-perl6.pgm') {   
    spurt $outfile, "P5\n$x $y\n$depth\n"; # .pgm header
    my $out = open( $outfile, :a, :bin ) or die "$!\n";
    $out.write( Blob.new(draw_sphere( ($x-1)/2, .9, .2) ) );
    $out.close;
}
 
sub normalize (@vec) { return @vec »/» ([+] @vec »*« @vec).sqrt }
 
sub dot (@x, @y) { return -([+] @x »*« @y) max 0 }
 
sub draw_sphere ( $rad, $k, $ambient ) {
    my @pixels;
    my $r2 = $rad * $rad;
    my @range = -$rad .. $rad;
    for flat @range X @range -> $x, $y {
        if (my $x2 = $x * $x) + (my $y2 = $y * $y) < $r2 {
            my @vector = normalize([$x, $y, ($r2 - $x2 - $y2).sqrt]);
            my $intensity = dot(@light, @vector) ** $k + $ambient;
            my $pixel = (0 max ($intensity * $depth).Int) min $depth;
            @pixels.push($pixel);
        }
        else {
            @pixels.push(0);
        }
    }
    return @pixels;
}
```