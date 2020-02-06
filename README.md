# inchi-isotopologue-extension
specification extension to InChi to better support isotopologue reporting

# Purpose:
Develop enhanced specifications within the regular InChI standard for representing isotopologues and isotopomers. More specifically, augment the isotopic layer specifications of the regular InChI standard so that specific isotopologues, isotopomers, partial isotopomers, and isotopologue fragments can be represented by a single InChI string and used to identify isotope-informative analytical features.

# Current Team Members:
* [Hunter Moseley](https://github.com/hunter-moseley) 
* [Philippe Rocca-Serra](https://github.com/proccaserra) 
* [Reza Salek](https://github.com/r7salek)
* [Masanori Arita](https://github.com/m-arita) 
* [Emma Schymanski](https://github.com/schymane)

# Problems Being Solved:
While the InChI standard has an isotopic layer for representing exact isotopomers, there is not a specification for representing a range (set) of isotopomers. The fundamental issue is that an ambiguous location of specific isotopes of certain atoms cannot be represented in the current standard.  This is needed to represent a set of isotopomers that correspond to a specific isotopologue.  Currently, an InChI string can represent a specific isotopomer, but not a set of mass-equivalent isotopomers.

- For example, here is the InChI string for alpha-D-glucopyranose:

`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: red; opacity: 0.80;" }

<p align="center"> C([C@@H]1[C@H]([C@@H]([C@H]([C@@H](O)O1)O)O)O)O</p>

- The following InChI string represents the explicit 13C isotopomer with the 4th carbon labeled:
<p align="center"> InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1<span style="color:red">/i1+0,2+0,3+0,4+1,5+0,6+0</span></p>

<p align="center"> [12CH2]([12C@@H]1[12C@H]([13C@@H]([12C@H]([12C@@H](O)O1)O)O)O)O</p>

However, there is no way to create a single valid InChI string that represents the isotopologue of alpha-D-glucopyranose containing one 13C atom at an undefined atomic location, which is the signal that would be observed in mass spectrometry experiments.  The use of multiple InChI strings to represent this is impractical for many isotopologues.

# Proposed Isotopologue Extension for InChI
The full proposal can be found [here](https://docs.google.com/document/d/1xh7lTWmwmuP0GF2Far6BREd-8g8Lh2FuSofE0d5tEXU/edit?usp=sharing).

# Community Feedback
We are actively seeking feedback on this proposal from the broader scientific community.

There are three ways to provide this feedback.

1. Post an issue on this repository.
2. Submit a comment via [this Google Form](https://goo.gl/forms/8lwvLJDae75bKobk2).
3. Create a PDF from the [full proposal](https://docs.google.com/document/d/1xh7lTWmwmuP0GF2Far6BREd-8g8Lh2FuSofE0d5tEXU/edit?usp=sharing), mark it up, and email it to: hunter.moseley@gmail.com
   * Please use the following subject line: "InChI Isotopologue Proposal Feedback".

# Tasks:
- Develop a more complete InChI isotopic layer specification and examples for isotopologues, isotopomers, partial isotopomers, and isotopologue fragments for naming isotopically-resolved molecular features detectable by analytical instrumentation.
- Develop InChI isotopic layer specification and examples for non-isotopically-resolved isotopologues detected by less resolved/accurate mass analytical instrumentation.
- Review and refine developed specifications.
- Present proposed specifications to the IUPAC InChI subcommittee and the InChI Trust.