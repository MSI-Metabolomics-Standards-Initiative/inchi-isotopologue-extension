## Current InChI Isotopomer Specification: 

1. Simple Definition: /i#<+|->#[I#],..

2. Complete Definition:

`/i<atom_number><isotope_designation>[<hydrogen_isotope><hydrogen_isotope_count>]`
`/i<atom_number>[<hydrogen_isotope><hydrogen_isotope_count>]`

where:

* <atom_number> - specific atom that has the specified isotope.
* <isotope_designation> - isotope designation indicated by a sign (+ or -) and number indicating the unit mass difference from the rounded average atomic mass of the element.

For example, the average atomic mass of Sn (118.710) is rounded to 119 and the most abundant isotope 120Sn is specified by “+1”.

* <hydrogen_isotope> - D for deuterium. etc.
* <hydrogen_isotope_count> - number of the specified hydrogen isotope bonded to the designated atom (<atom_number>); 1 if omitted.  

## Examples:

1. 13C at carbons 1 and 2 in alpha-D-glucopyranose:

`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1/i1+1,2+1`

2. 13C at carbon 1 with 2H2 attached in alpha-D-glucopyranose:

`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1/i1+1D2`

3. Carbon 1 with 2H2 attached in alpha-D-glucopyranose:

`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1/i1D2`

4. 13C at carbon 1 with 2H1 attached in alpha-D-glucopyranose:

`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1/i1D/t1?,2-,3-,4+,5-,6+`

Technically, this is an isotopologue fragment and not an isotopomer, meaning there is limited ambiguity in the location of the deuterium isotope.  

5. 2H bonded to carbon 1 in a stereospecific configuration in alpha-D-glucopyranose:

`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1/i1D/t1-,2-,3-,4+,5-,6+`

This is a stereospecific isotopomer.  

6. 2H bonded to all heteroatoms of alpha-D-glucopyranose (as e.g. in exchange experiments):

`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1/i7D,8D,9D,10D, 11D`


