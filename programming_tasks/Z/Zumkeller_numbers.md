[1]: https://rosettacode.org/wiki/Zumkeller_numbers

# [Zumkeller numbers][1]

```perl
use ntheory:from<Perl5> <factor is_prime>;
 
sub zumkeller ($range)  {
    $range.grep: -> $maybe {
        next if $maybe < 3;
        next if $maybe.&is_prime;
        my @divisors = $maybe.&factor.combinations».reduce( &[*] ).unique.reverse;
        next unless [&&] +@divisors > 2, +@divisors %% 2, (my $sum = sum @divisors) %% 2, ($sum /= 2) >= $maybe;
        my $zumkeller = False;
        if $maybe % 2 {
            $zumkeller = True
        } else {
            TEST: loop (my $c = 1; $c < @divisors / 2; ++$c) {
                @divisors.combinations($c).map: -> $d {
                    next if (sum $d) != $sum;
                    $zumkeller = True and last TEST;
                }
            }
        }
        $zumkeller
    }
}
 
say "First 220 Zumkeller numbers:\n" ~
    zumkeller(^Inf)[^220].rotor(20)».fmt('%3d').join: "\n";
 
put "\nFirst 40 odd Zumkeller numbers:\n" ~
    zumkeller((^Inf).map: * * 2 + 1)[^40].rotor(10)».fmt('%7d').join: "\n";
 
# Stretch. Slow to calculate. (minutes) 
put "\nFirst 40 odd Zumkeller numbers not divisible by 5:\n" ~
    zumkeller(flat (^Inf).map: {my \p = 10 * $_; p+1, p+3, p+7, p+9} )[^40].rotor(10)».fmt('%7d').join: "\n";
```

#### Output:
```
First 220 Zumkeller numbers:
  6  12  20  24  28  30  40  42  48  54  56  60  66  70  78  80  84  88  90  96
102 104 108 112 114 120 126 132 138 140 150 156 160 168 174 176 180 186 192 198
204 208 210 216 220 222 224 228 234 240 246 252 258 260 264 270 272 276 280 282
294 300 304 306 308 312 318 320 330 336 340 342 348 350 352 354 360 364 366 368
372 378 380 384 390 396 402 408 414 416 420 426 432 438 440 444 448 456 460 462
464 468 474 476 480 486 490 492 496 498 500 504 510 516 520 522 528 532 534 540
544 546 550 552 558 560 564 570 572 580 582 588 594 600 606 608 612 616 618 620
624 630 636 640 642 644 650 654 660 666 672 678 680 684 690 696 700 702 704 708
714 720 726 728 732 736 740 744 750 756 760 762 768 770 780 786 792 798 804 810
812 816 820 822 828 832 834 836 840 852 858 860 864 868 870 876 880 888 894 896
906 910 912 918 920 924 928 930 936 940 942 945 948 952 960 966 972 978 980 984

First 40 odd Zumkeller numbers:
    945    1575    2205    2835    3465    4095    4725    5355    5775    5985
   6435    6615    6825    7245    7425    7875    8085    8415    8505    8925
   9135    9555    9765   10395   11655   12285   12705   12915   13545   14175
  14805   15015   15435   16065   16695   17325   17955   18585   19215   19305

First 40 odd Zumkeller numbers not divisible by 5:
  81081  153153  171171  189189  207207  223839  243243  261261  279279  297297
 351351  459459  513513  567567  621621  671517  729729  742203  783783  793611
 812889  837837  891891  908523  960687  999999 1024947 1054053 1072071 1073709
1095633 1108107 1145529 1162161 1198197 1224531 1270269 1307691 1324323 1378377
```