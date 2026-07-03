# Algorithm-Time-ToNumber

Convert time to a number.

- circle :: return two angles suitable for use as two features with isolation forest

- angle :: similar to circle, but only one angle... produces a consistent range but will
  overlap with it's self

- noon_fail :: Wraps at 00:00 but will produce a gap at 12:00.

- midnight_fail :: Wraps at 12:00 but will produce a gap at 00:00.

The one you likely want is circle.

So when using it with isolation forest you will have each returned angle be it's own
feature for a  row. While each feature will overlap with it's self at a point, the use of
two helps avoid the clustering issue.


```perl
    use Algorithm::Time::ToNumber;

    print "---------------------------------------------------\n";
    print "------------------noon_fail------------------------\n";
    print "---------------------------------------------------\n";

    my $hour=0;
    while ($hour < 24) {
        my $time = $hour . ':00';
        print $time . ' ' . Algorithm::Time::ToNumber->noon_fail($time) . "\n";

        $time = $hour . ':30';
        print $time . ' ' . Algorithm::Time::ToNumber->noon_fail($time) . "\n";

        $hour++;
    }

    print "---------------------------------------------------\n";
    print "----------------midnight_fail----------------------\n";
    print "---------------------------------------------------\n";

    $hour=0;
    while ($hour < 24) {
        my $time = $hour . ':00';
        print $time . ' ' . Algorithm::Time::ToNumber->midnight_fail($time) . "\n";

        $time = $hour . ':30';
        print $time . ' ' . Algorithm::Time::ToNumber->midnight_fail($time) . "\n";

        $hour++;
    }

    print "---------------------------------------------------\n";
    print "---------------------circle------------------------\n";
    print "---------------------------------------------------\n";

    # this is what you want if you plan to use it with isolation forest

    $hour=0;
    while ($hour < 24) {
        my $time = $hour . ':00';
        my ($sin_angle, $cos_angle) = Algorithm::Time::ToNumber->circle($time);
        print $time . ' ' . $sin_angle . ' ' . $cos_angle . "\n";

        $time = $hour . ':30';
        ($sin_angle, $cos_angle) = Algorithm::Time::ToNumber->circle($time);
        print $time . ' ' . $sin_angle . ' ' . $cos_angle . "\n";

        $hour++;
    }

    print "---------------------------------------------------\n";
    print "----------------------angle------------------------\n";
    print "---------------------------------------------------\n";

    $hour=0;
    while ($hour < 24) {
        my $time = $hour . ':00';
        my ($sin_angle) = Algorithm::Time::ToNumber->circle($time);
        print $time . ' ' . $sin_angle . "\n";

        $time = $hour . ':30';
        ($sin_angle, $cos_angle) = Algorithm::Time::ToNumber->circle($time);
        print $time . ' ' . $sin_angle . "\n";

        $hour++;
    }
```

# Install

## Source

```shell
perl Makefile.PL
make
make test
make install
```

## FreeBSD

```shell
pkg install p5-App-cpanminus
cpanm Algorithm::Time::ToNumber
```

## Debian

```shell
apt-get install cpanminus
cpanm Algorithm::Time::ToNumber
```
