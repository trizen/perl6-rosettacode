[1]: https://rosettacode.org/wiki/Integer_comparison

# [Integer comparison][1]

```raku
my $a = prompt("1st int: ").floor;
my $b = prompt("2nd int: ").floor;
 
if $a < $b {
    say 'Less';
}
elsif $a > $b {
    say 'Greater';
}
elsif $a == $b {
    say 'Equal';
}
```


With `<=>`:

```raku
say <Less Equal Greater>[($a <=> $b) + 1];
```


A three-way comparison such as `<=>` actually returns an `Order` enum which stringifies into 'Decrease', 'Increase' or 'Same'. So if it's ok to use this particular vocabulary, you could say that this task is actually a built in:

```raku
say prompt("1st int: ") <=> prompt("2nd int: ");
```