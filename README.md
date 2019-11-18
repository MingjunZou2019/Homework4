# Homework4
$title A Crude Oil Transport Model

Set
   i 'supply center' / Cushing, NewOrleans, Houston /
   j 'markets'        / Tulsa /;

Parameter
   a(i) 'WTI capacity of supply center i (bbl)'
        / Cushing     30
          NewOrleans  0
          Houston     200/

   b(i) 'Brent capacity of supply center i (bbl)'
        / Cushing     20
          NewOrleans  500
          Houston     0/;

   c(j) 'oil demand at refinery location (bbl)'
      / Tulsa       500 /;

Table d(i,j) 'cost of transportation of unit barrel of oil from supply center to refinery ($/bbl)'
              Tulsa
   Cushing      2
   NewOrleans  45
   Houston     40 ;

Variable
   x(i,j) 'amount of oil transported in barrels'
   z      'total transportation costs in dollars';

Positive Variable x;

Equation
   cost      'define objective function'
   supply(i) 'observe supply limit at center i'
   demand(j) 'satisfy demand at refinery j';

cost..      z =e= sum((i,j), c(i,j)*x(i,j));

supply(i).. sum(j, x(i,j)) =l= a(i);

demand(j).. sum(i, x(i,j)) =g= b(j);

Model Gasselection / all /;

solve Gasselection using lp minimizing z;

display x.i, x.j;
