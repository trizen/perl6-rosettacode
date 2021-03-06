[1]: https://rosettacode.org/wiki/Sorting_algorithms/Merge_sort

# [Sorting algorithms/Merge sort][1]

```perl
sub merge_sort ( @a ) {
    return @a if @a <= 1;
 
    my $m = @a.elems div 2;
    my @l = flat merge_sort @a[  0 ..^ $m ];
    my @r = flat merge_sort @a[ $m ..^ @a ];
 
    return flat @l, @r if @l[*-1] !after @r[0];
    return flat gather {
        take @l[0] before @r[0] ?? @l.shift !! @r.shift
            while @l and @r;
        take @l, @r;
    }
}
my @data = 6, 7, 2, 1, 8, 9, 5, 3, 4;
say 'input  = ' ~ @data;
say 'output = ' ~ @data.&merge_sort;
```

#### Output:
```
input  = 6 7 2 1 8 9 5 3 4
output = 1 2 3 4 5 6 7 8 9
```