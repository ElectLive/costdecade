# costdecade

Price durability by the decade, not the receipt.

Cheap gear replaced three times can cost more than the dear piece bought
once, but nobody runs that arithmetic at the shelf. costdecade does it in
one line: give each candidate a price and how long it lasts, and the tool
ranks the field by real cost per decade, finds the exact lifespan where the
dearer option starts winning, and totals the spend over a full ownership
horizon with replacement inflation on top. A CSV of candidates for one
category goes in, a ranked verdict comes out, including the cases where the
budget pick beats the heirloom one.

## Use

    $ python3 costdecade.py --price 340 --life 10 --rival-price 120 --rival-life 2
    cost per decade, ranked  (horizon 30y, inflation 0.0%)
      item                   $  340.00/decade   $  34.00/yr   $ 1020.00 over 30y
      rival                  $  600.00/decade   $  60.00/yr   $ 1800.00 over 30y
      break-even: rival must last 3.5 years to win
      winner: item

    $ python3 costdecade.py --file sample_candidates.csv --horizon 30 --inflation 3
    cost per decade, ranked  (horizon 30y, inflation 3.0%)
      Steel flask            $   37.50/decade   $   3.75/yr   $   139.09 over 30y
      Merino sock pair       $   42.50/decade   $   4.25/yr   $   142.24 over 30y
      Ceramic mug            $   52.00/decade   $   5.20/yr   $   168.18 over 30y
      Durable espresso machine $  226.67/decade   $  22.67/yr   $   690.20 over 30y
      Budget dual boiler     $  600.00/decade   $  60.00/yr   $  2231.87 over 30y
      winner: Steel flask

    $ python3 costdecade.py --file sample_candidates.csv --horizon 30 --json

Exit code 0 when a budget passed with --budget is met, 1 when the winner
still costs more than the budget allows, so a whole catalog of categories
can be checked mechanically.

## What the sample says

sample_candidates.csv ships in this repo and every figure below comes from
a real run of the tool.

- A $120 dual boiler lasting 2 years costs $600 per decade and $2,231.87
  over 30 years at 3% replacement inflation. A $340 machine lasting 15
  years costs $226.67 per decade and $690.20 over the same horizon. The
  durable machine finishes $1,541.67 ahead.
- The crossover is short. At $34 per year of service, the $340 machine
  needs the cheap boiler to last just 3.5 years to lose; it lasts 2.
- Warranty years count. A row's service life never drops below its written
  warranty, because the warranty is the one lifespan claim a maker backs
  with money.

## Method notes

- Cost per decade is effective price divided by service life, scaled to ten
  years. Pass --resale to credit salvage value at end of life.
- Horizon totals replace items on the same cadence with prices inflating at
  your rate, which falls hardest on short-lived gear.
- Lifespans are estimates, and the tool leaves them that way: estimates in,
  verdicts out. The point is that the comparison happen in numbers.

MIT licensed. From Poket Dev.
