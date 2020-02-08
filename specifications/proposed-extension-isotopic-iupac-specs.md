# Proposal for New Isotopologue and Isotopomer Specifications

In the following proposed specifications, isotopologue designations are indicated by parentheses with the element identified first, while isotopomer designations lack parentheses with the atom position identified first: e.g. /a(C2+1) for isotopologue and /i7+1 for isotopomer. 
The lack of parentheses for isotopomers ensures backwards compatibility with previous InChI specifications. See individual specifications below for details.


## Isotopically-Resolved Isotopologue Specification: 

* Rationale: to enable the use of InChI to specify an isotopologue or isotopologue fragment.

* Simple Definition:  `/a(Ee#<+|->#[,#]...)`

* Complete Definition:  `/a(<element><isotope_count><isotope_designation>[,<atom_number>])`

	* <element> one or two letter Element code (Ee).
	* <isotope_count> number of atoms with the designated isotope (#).
	* <isotope_designation> isotope designation indicated by a sign (+ or -) and number indicating the unit mass difference from the rounded average atomic mass of the element. 
	For example, the average atomic mass of Sn (118.710) is rounded to 119. 
	We specify two <sup>118</sup>Sn atoms as `/a(Sn2-1)`.
	* <atom_number> specific atom(s) that may have the specified isotope.  If empty, then all atoms of the given element may have the specified isotope (# in [,#]).

If multiple atoms need to be specified, these are comma separated. 

* Regular Expression Definition: `[/]a[(][A-Z][a-z]?\d+[+-]\d+([,]\d+)*[)]`

* Examples:

	1. <sup>13</sup>C<sub>2</sub> isotopologue of alpha-D-glucopyranose:

		`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{:style="color: black; opacity: 0.80;"}`/a(C2+1)`{:style="color: red; opacity: 0.80;"}

	2. <sup>13</sup>C<sub>2</sub><sup>2</sup>H<sub>3</sub> isotopologue of alpha-D-glucopyranose:

		`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;"}`/a(C2+1),(H3+1)`{: style="color: red; opacity: 0.80;"}

	3. <sup>17</sup>O<sub>2</sub><sup>18</sup>O<sub>1</sub> isotopologue of alpha-D-glucopyranose:

		`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/a(O2+1),(O1+2)`{: style="color: red; opacity: 0.80;" }

	4. <sup>13</sup>C<sub>2</sub> limited to atoms 4,5,6 isotopologue fragment of alpha-D-glucopyranose:	

		`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/a(C2+1,4,5,6)`{: style="color: red; opacity: 0.80;" }

	5. <sup>13</sup>C<sub>1</sub> at atom 1, 2H1 limited to atoms 13,14 isotopologue fragment of alpha-D-glucopyranose:

		`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1/i1+1`{: style="color: black; opacity: 0.80;" }`/a(H1+1,13,14)`{: style="color: red; opacity: 0.80;" }

	6. <sup>13</sup>C<sub>2</sub><sup>15</sup>N<sub>1</sub> isotopologue of 2-Amino-2-deoxy-6-O-phosphono-alpha-D-glucopyranose

		`InChI=1/C6H14NO8P/c7-3-5(9)4(8)2(15-6(3)10)1-14-16(11,12)13/h2-6,8-10H,1,7H2,(H2,11,12,13)/t2-,3-,4-,5-,6+/m1/s1/i7+1`{: style="color: black; opacity: 0.80;" }`/a(C2+1)`{: style="color: red; opacity: 0.80;" }

Notice the combination of isotopologue and isotopomer specification, since there is only 1 nitrogen atom in the molecule.

Therefore when ambiguity of isotope location is present, it is clearly indicated in the isotopic layer.


## Augmented Range Specification: 

* Simple Isotopologue Definition: `/a(Ee#<+|->#[,#-#|,#]...)`

* Complete Isotopologue Definition: `/a(<element><isotope_count><isotope_designation>[,<start_atom_number>-<end_atom_number>])`

* Simple Isotopomer Definition: `/i#-#<+|->#`

The augmented isotopomer range specification is limited to a single `atom_range` and `isotope_designation`, due to parsing ambiguities that would arise if mixed `atom_range` and single atom designations were allowed.

* Complete Isotopomer Definition: `/i<start_atom_number>-<end_atom_number><isotope_designation>`

* Examples:

	1. <sup>13</sup>C<sub>2</sub> limited to atoms 4,5,6 isotopologue fragment of alpha-D-glucopyranose:

		`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/a(C2+1,4-6)`{: style="color: red; opacity: 0.80;" }

	2. <sup>13</sup>C<sub>6</sub> isotopomer of alpha-D-glucopyranose:

		`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/i1-6+1`{: style="color: red; opacity: 0.80;" }


## Nominal-Mass Isotopologue Specification: 

* Rationale: to enable an InChI representation for mass spectral features that are not isotope-resolved.

* Simple Nominal-Mass Isotopologue Definition: `/a(#n[,#]...)`

* Complete Nominal-Mass Isotopologue Definition: `/a(<neutron_count>n[,<atom_number>])`
	
	<neutron_count> - number of neutrons of extra mass.

Notice the reversal of `neutron_count` relative to the `n` representing neutron.  This is done so that no ambiguity will exist with the isotopically-resolved isotopologue specification, where the element is indicated first and the `isotope_count` second. 

* Examples:

	1. M+3 isotopologue of alpha-D-glucopyranose:

		`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/a(3n)`{: style="color: red; opacity: 0.80;" }

	The lack of a specified list of atoms indicates the whole molecule.

	2. M+4 isotopologue limited to carbon atoms of alpha-D-glucopyranose:

		`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/a(4n,1,2,3,4,5,6)`{: style="color: red; opacity: 0.80;" }

		With augmented range specifications:

		`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/i(4n,1-6)`{: style="color: red; opacity: 0.80;" }
		
		**This situation could arise from use of tandem mass spectrometry features that localize the extra mass to certain elements.** 


## Partial Isotopomer Specification: 

* Rationale: to enable an InChI representation of a partial isotopomer, which is directly useful for describing most individual nuclear magnetic resonance spectroscopy spectral features.

* Simple Definition: same as the full isotopomer specification but with the unknown isotope specifications removed (Example 2). 
	
	The designation of the isotope for all atoms of a given element will represent a full isotopomer (Example 1). 

* Examples:
	1. <sup>13</sup>C at 4th carbon for full isotopomer (with respect to carbon) of alpha-D-glucopyranose:

		`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/i1+0,2+0,3+0,4+1,5+0,6+0`{: style="color: red; opacity: 0.80;" }

		With augmented range specification: 

		`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/i1-3+0,4+1,5-6+0`{: style="color: red; opacity: 0.80;" }

	2. <sup>13</sup>C at 4th carbon for partial isotopomer of alpha-D-glucopyranose:

		`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/i4+1`{: style="color: red; opacity: 0.80;" }

		Only the atom with the known isotopic composition is indicated.


## Cross-Constitutional Isomer Isotopologue Specification: 

* Rationale: to enable a non-standard InChI representation of isotopologues that span multiple constitutional isomers, i.e. either a fully or partially isotopically-resolved molecular formula. 

		**This specification is directly useful for describing individual features in mass spectrometry when the specific constitutional isomer is unknown.**

* Simple Definition: `1/Ee#[Ee#].../a(Ee#<+|->#) OR 1/Ee#[Ee#].../a(#n)`

* Examples:
	1. <sup>13</sup>C<sub>2</sub> isotopologue of molecules with molecular formula C<sub>6</sub>H<sub>12</sub>O<sub>6</sub>:

		`InChI=1/C6H12O6/`{: style="color: black; opacity: 0.80;" }`/a(C2+1)`{: style="color: red; opacity: 0.80;" }

	2. <sup>13</sup>C<sub>1</sub><sup>18</sup>O<sub>1</sub> isotopologue of molecules with molecular formula C<sub>6</sub>H<sub>12</sub>O<sub>6</sub>:

		`InChI=1/C6H12O6/`{: style="color: black; opacity: 0.80;" }`/a(C2+1),(O1+2)`{: style="color: red; opacity: 0.80;" }

	3. M+3 isotopologue of molecules with molecular formula C<sub>6</sub>H<sub>12</sub>O<sub>6</sub>:

		`InChI=1/C6H12O6/`{: style="color: black; opacity: 0.80;" }`/a(3n)`{: style="color: red; opacity: 0.80;" }

		**This last example enables a major use-case in mass spectrometry spectral feature assignment**.
