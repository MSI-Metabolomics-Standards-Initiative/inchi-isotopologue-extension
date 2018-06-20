# inchi-isotopologue-extension
specification extension to InChi to better support isotopologue reporting

# Purpose:
Develop enhanced specifications within the regular InChI standard for representing isotopologues and isotopomers. More specifically, augment the isotopic layer specifications of the regular InChI standard so that specific isotopologues, isotopomers, partial isotopomers, and isotopologue fragments can be represented by a single InChI string and used to identify isotope-informative analytical features.

# Current Team Members:
* [Hunter Moseley](http://www.github.com/hunter-moseley) 
* [Philippe Rocca-Serra](http://www.github.com/proccaserra) 
* [Reza Salek](http://www.github.com/rsalek)
* [Masanori Arita](http://www.github.com/m-arita) 
* [Emma Schymanski](http://www.github.com/schymane)

# Problems Being Solved:
While the InChI standard has an isotopic layer for representing exact isotopomers, there is not a specification for representing a range (set) of isotopomers. The fundamental issue is that an ambiguous location of specific isotopes of certain atoms cannot be represented in the current standard.  This is needed to represent a set of isotopomers that correspond to a specific isotopologue.  Currently, an InChI string can represent a specific isotopomer, but not a set of mass-equivalent isotopomers.

- For example, here is the InChI string for alpha-D-glucopyranose:
>`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1
C([C@@H]1[C@H]([C@@H]([C@H]([C@@H](O)O1)O)O)O)O`
- The following InChI string represents the explicit 13C isotopomer with the 4th carbon labeled:
>`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1/i1+0,2+0,3+0,4+1,5+0,6+0
[12CH2]([12C@@H]1[12C@H]([13C@@H]([12C@H]([12C@@H](O)O1)O)O)O)O`

The isotopic layer is highlighted in red. However, there is no way to create a single valid InChI string that represents the isotopologue of alpha-D-glucopyranose containing one 13C atom at an undefined atomic location, which is the signal that would be observed in mass spectrometry experiments.  The use of multiple InChI strings to represent this is impractical for many isotopologues.

# Tasks:
- Develop a more complete InChI isotopic layer specification and examples for isotopologues, isotopomers, partial isotopomers, and isotopologue fragments for naming isotopically-resolved molecular features detectable by analytical instrumentation.
- Develop InChI isotopic layer specification and examples for non-isotopically-resolved isotopologues detected by less resolved/accurate mass analytical instrumentation.
- Review and refine developed specifications.
- Present proposed specifications to the IUPAC InChI subcommittee and the InChI Trust.

# Definitions:
- **Isotopomer** - also known as isotopic isomers, these are isomers with the same number of each isotope of each element but differing in their positions within the chemical structure. Isotopomers can also be specific to stereochemistry, where they are known as isotopic stereoisomers.  By definition, isotopomers have the same mass, since they have the same isotopic composition.  However, the set of all isotopomers which span all possible isotopic compositions are often collectively referred to as isotopomers.  
- **Partial Isotopomer** - part of an isotopomer where the isotopic content of specific atoms is known.  In nuclear magnetic resonance spectroscopy (NMR) and in rare circumstances in tandem mass spectrometry, individual spectral features may directly indicate that certain atoms of a particular molecule have certain isotopes.  As an example from NMR, certain analytical features may indicate that carbon 1 of alpha-D-glucopyranose is 13C labeled without knowing the isotopic status of the other carbon atoms.
- **Isotopologue** - representing molecules of the same chemical entity and same isotopic composition. Related isotopologues represent the same chemical entity but differ in the isotopic composition.  A single isotopologue represents a set of mass-equivalent isotopomers. 
- **Isotopologue Fragment** - a refined set of isotopomers where the ambiguity of isotope location is limited to a subset of the atoms. This is a subset of the mass-equivalent isotopomers representing the full isotopologue. Tandem mass spectrometry may provide spectral features that indicate where (possibly mixed) isotopes are localized within a chemical structure.  


