## Questions and Issues Posed by the IUPAC InChI Subcommittee

# Question 1:
 How will be stereochemistry covered, if it changes with hopping the isotopes (e.g. 2 x 13C in inositol). In regards to stereochemistry, non-standard InChi can distinguish between ‘undefined’ and ‘unknown’, will the isotopic enhancement cover similar cases?


# *Answer*:
The answer is ‘undefined’ for stereochemistry created by the presence of isotope.  Since the isotopologue represents a set of isotopomers, each isotopomer may have a specific stereochemistry based on specific isotope location.  It is not that they are necessarily ‘unknown’, but the set can create a situation where there is not a single completely designated stereochemistry.  For the stereochemistry not specified by isotope, this would naturally be included with the isotopologue designation, as illustrated in the following examples:

[https://comptox.epa.gov/dashboard/dsstoxdb/results?search=inositol](https://comptox.epa.gov/dashboard/dsstoxdb/results?search=inositol)

`InChI=1S/C6H12O6/c7-1-2(8)4(10)6(12)5(11)3(1)9/h1-12H`

[https://comptox.epa.gov/dashboard/dsstoxdb/results?search=myo-Inositol](https://comptox.epa.gov/dashboard/dsstoxdb/results?search=myo-Inositol)

`InChI=1S/C6H12O6/c7-1-2(8)4(10)6(12)5(11)3(1)9/h1-12H/t1-,2-,3-,4+,5-,6-`

The InChI strings for 13C2 isotopologues of inositol and myo-inositol would be:

`InChI=1/C6H12O6/c7-1-2(8)4(10)6(12)5(11)3(1)9/h1-12H`{: style="color: black; opacity: 0.80;" }`/a(C2+1)`{: style="color: red; opacity: 0.80;" }
`InChI=1/C6H12O6/c7-1-2(8)4(10)6(12)5(11)3(1)9/h1-12H/t1-,2-,3-,4+,5-,6-`{: style="color: black; opacity: 0.80;" }`/a(C2+1)`{: style="color: red; opacity: 0.80;" }

# Question 2:
 Is canonicalization depending on the mass (as in the case of inositol)?


# *Answer*:
For the most part, the current InChI canonicalization algorithm creates a unique numbering that is isotope agnostic. However, problems arise when dealing with stereospecific isotopomers involving hydrogen. The canonicalization algorithm will generate the same atom numbering for two different stereospecific hydrogen isotopomers.
The following is an example:

`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/i1D/t1-,2-,3-,4+,5-,6+`{: style="color: red; opacity: 0.80;" }

`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/i1D/t1-,2+,3+,4-,5+,6-/m0`{: style="color: red; opacity: 0.80;" }

The canonicalization algorithm in the InChI Trust software will generate identical MOL/SDF files with the deuteration indicated on atom number 13. Open Babel’s “--gen3D” option has a segmentation fault, so the unique stereochemistry cannot be retrieved via that software. The Biological Magnetic Resonance Bank has been working on an approach called ALATIS to generate unique hydrogen atom numbering, but their solution is not practical for everyday use of InChI. It would be best that the canonicalization algorithm in the InChI Trust software at least generated unique atom numbering for stereospecific hydrogen isotopomers. An issue (#1794) has been posted on the Open Babel GitHub repository, so maybe a stereospecific MOL/SDF file could be generated from their software if they fix their bug.  

# Question 3: 
It is still about only 1 molecule, not a mixture? One molecule (partially defined) is acceptable; mixtures are more problematic and are being covered in a different project and code base

# *Answer*:
The current proposed specifications are mainly for one molecule; however, the cross-constitutional isomer isotopologue specification could represent a mixture of structural isomers with the same mass, as only the formula is defined.

# Question 4:
There is a potential overlap with variable structure proposal; the isotopologue proposal is asking a different and more specific question. Revision on the variable structure proposal could, potentially, allow for unspecified positions to include isotopologues.


# *Answer*:
We suspect that “dividing and conquering” (treating both cases in the separate sub-groups then ensuring compatibility of the developed approaches) may be a better strategy, since we have specifications to handle nominal mass and across (all) constitutional isomers. The nominal mass situation will likely be hard to handle in the variable structure proposal. The cross-constitutional isomer situation is probably handling a much wider range of variable structures than what the variable structure proposal is focused on handling. It would be good for some of our team to directly interact with the team developing the variable structure proposal to discuss this.

# Question 5:
What input format was suggested to feed InChI with an isotoplogue, which has uncertain positions of isotopic atoms?
For instance, consider two Deuterium atoms located in any two out of 5 hydroxyl groups in a molecule. Of course, the  examples may be much more complicated.
As far as I know, molfile formats, which are currently used to feed InChI with chemical structures, cannot express such an isotopologue (I think that query formats should not be used)
IMHO, no software development is possible without a suitable well-defined input format,  a representative test set of isotopologues expressed in the suggested format,  and their suggested InChI.

# *Answer*: 
The ideal solution is to extend the MOL file format to include options for specifying ambiguous isotope location.  However, such development and standardization is probably beyond scope of the current proposal development for InChI isotopologue specifications.  This is due to the history of the CT File Format, the parent MOL file format which was released by MDL Information Systems and through a series of acquisitions is now part of the BioVia unit of Dassault Systèmes.  Is there even a formal process to extend the MOL file format and how would such an extension be disseminated? If a formal extension process for CT/MOL files can be found or established, we would be willing to initiate the development of extensions to the MOL file format that facilitate direct representation of isotopologues. 

As an alternative, an SDF file could be used to provide a complete description of an isotopologue.  This approach is functional and would be completely descriptive of an isotopologue by providing an enumeration of all isotopomers represented by a given isotopologue.  It also holds to the concept that a single MOL file can represent a single isotopomer, while an isotopologue represents a compatible set of isotopomers that must be represented as a set.  Here are two possible SDF representations that would be adequate:
Including MOL files for all specific isotopomers represented by the isotopologue.
Including masking MOL files for each isotope present that indicate the ambiguous location of isotope along with additional information in the SDF file to indicate the number of each isotope present for a given masking MOL file.  The SDF file would also include partial isotopomer MOL files for isotope that is unambiguous in its location.
Such SDF file representations could be used both as an input format and for visualization purposes.  Hunter Moseley’s lab has an open codebase available on GitHub that can generate type-A SDF files:
[https://github.com/MoseleyBioinformaticsLab/isoenum](https://github.com/MoseleyBioinformaticsLab/isoenum).
His lab is willing to extend the codebase to generate type-B SDF files as a demonstration of these isotopologue representing SDF files, which would be better for visualization purposes.

# Question 6:
To make the isotopologue InChI usable and adopted by masses, in addition to the well-defined input format an isotopologue chemical structure editor/viewer is a must. This requires a simple and easy to understand concept of visualization of any complexity isotopologues. Of course the editing is out of InChI project scope. However, the visualization concept may be required for extending winchi  to isotopologues.

# *Answer*:
See answer to Question 5.

# Question 7:
The most serious concern I have is a mixture of "known" and "unknown" things appearing in the same /i layer, as the proposal presumes.

It is based on idea that a single /i layer is covering both isotopomer (precisely known) and isotopologue (unknown or unprecise) information.

InChI typically tries to employ somewhat different general design, which has some added benefits. 
Namely, it first includes some layer capturing an unprecise information, then optionally includes its extension/analog, which accounts for more precise info. 
This layered approach allows one to represent molecular information with a different degree of percisiness.

The example is tautomeric data [e.g., [https://www.inchi-trust.org/technical-faq/#6.1](https://www.inchi-trust.org/technical-faq/#6.1)

InChI string contains /h sub-layer in main layer, which lists all possible locations of mobile H's -- but not the precise locations themselves. However, the exact locations may be further specified by /h sub-layer in FixedH layer, following /f.
Most notably, you may cut longer ("precise" mobile H) InChI at /f and retain only the beginning: this would be valid ("unprecise" mobile H) parent of all possible longer strings representing tautomers.

Ideally, it would be most convenient to have such a layout at least partially preserved for the hierarchy comprising isotopologues, mass-equivalent isotopomers, nominal-mass isotopoologues, and isotope-position-distinct isotopomers, etc. Current design in the proposal does not reflect such "parent"/"child", or "generic"/"specific" relations, at least represented in easily deducible manner.

I am not sure if it is really/easily achievable, but I would strongly suggest that the authors consider a possibility of introducing the layered hierarchical isotopologue/isomer layout, at least partially.

# *Answer*:
We will separate precise isotopomer specification from isotopologue specification using a separate layer “/a” for ambiguous location of isotope. We have updated the specification accordingly - assuming that “/a” is not being used by current or other proposed InChI specifications.

# Question 8:
Another thing I am not happy with is that combined isotopologue-isotopomer layer may eventually break the hierarchy already implemented in InChI.

Consider an interplay of isotopes and stereo. In general, "unprecise" indication of isotope position [isotopologue] may either (a) result in (change of) stereochemistry or (b) does not touch any stereochemical feature. However, it may be very difficult to distinguish between (a) and (b), as this would require full enumeration and analysis of the whole set of available isotopomers. 

So the only reasonable option is to consider all stereo "appearing after" /i as unreliable/undefined (as is correctly specified in answers of the authors to some previous question, end of the proposal).
What is the worse, sometimes (when /i does not cover isotopologues but only precise isotopomers) old logics would still work and stereo "appearing after" /i would be absolutely legitimate.

Moreover, any other stereo features "appearing further at right", in InChI string (e.g., due to tautomerism with /f exact H positions, which are normally accounted for), would also be effectively invalidated by isotopologue-enabled /i layer...


# *Answer*:
The separation of isotopomer and isotopologue specifications into separate layers (see above) should help make it more obvious when the isotope touches stereochemical features.  Also, a full enumeration of isotopomers is not needed to distinguish between between changed (undefined) stereochemistry or untouched stereochemistry. Stereochemistry created by precise isotopomer designation will be undefined if another atom bonded to the created stereocenter has ambiguous isotope designation involving the same element of the isotopomer designation.   

# Question 9:
The proposal suggests that "isotopologue designations are indicated by parentheses with the element identified first, while isotopomer designations lack parentheses with the atom position identified first: e.g. /i( C2 +1) for isotopologue and /i 7 +1 for isotopomer."

I would strongly object to the usage of element symbols here (and it's also the opinion of DT with whom we briefly chatted). 

Currently, InChI contains element symbols only in the very first, formula layer. In all other contexts, atoms are referred to by their numbers.
It may seems convenient for specific purpose of the moment, but preserving some design principles is more important in a long run...


# *Answer*:
We understand the need for adhering to design principles; however the current design principles were primarily based on designation of characteristics to specific atoms.  By extending the InChI to cover ambiguous designation, the design principles may need to be revisited to achieve a balance between the original concept and a compact, understandable representation.  The specification of the element prevents the need for specifying a collection of atoms.  For instance, we currently propose to represent two 13C located somewhere across all carbon atoms as:
     `InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/a(C2+1)`

Here are some alternatives specifications that are not as concise nor as easy to interpret:

`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/a(2+1,1,2,3,4,5,6)`{: style="color: red; opacity: 0.80;" }

OR

`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/a(2+1,1-6)`{: style="color: red; opacity: 0.80;" }

We could still represent nominal-mass isotopologues of 3 neutrons spread across the molecule as:

`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/a(3n)`{: style="color: red; opacity: 0.80;" }

OR (if we change the original specification to be more consistent with this new alternative)

`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/a(3+n)`{: style="color: red; opacity: 0.80;" }

OR

`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/a(3+n,1-24)`{: style="color: red; opacity: 0.80;" }

Here is an example of 3 neutrons spread across the non-hydrogen atoms:

`InChI=1/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/a(3+n,1-12)`{: style="color: red; opacity: 0.80;" }

But cross-constitutional isomer isotopologues cannot be represented unless we assume some ordering of atoms like the typical C/ascending atomic number/H ordering seen generated by the InChI Foundation software:

      `InChI=1/C6H12O6`{: style="color: black; opacity: 0.80;" }`/a(2+1,1,2,3,4,5,6)`{: style="color: red; opacity: 0.80;" }
      `InChI=1/C6H12O6`{: style="color: black; opacity: 0.80;" }`/a(2+1,1-6)`{: style="color: red; opacity: 0.80;" }


# Question 10:
Minor issues.
(a)
"The following InChI string represents the explicit 13 C isotopomer with the 4th carbon labeled:
`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1 /i1+0,2+0,3+0,4+1,5+0,6+0"`

Actually, this represents the explicit 13 C isotopomer with the 4th carbon labeled and the explicit 12C "labeling" for all the other carbons.
Construct "+0" always means that that the atom is of a specific isotope whose mass number is the same as the rounded average atomic mass.
[https://www.inchi-trust.org/technical-faq/#9.3](https://www.inchi-trust.org/technical-faq/#9.3)


# *Answer*:
We are proposing that “/i4+1” refers to the partial isotopomer designation and that  “/i1+0,2+0,3+0,4+1,5+0,6+0" refers to the fully specified isotopomer designation. This was shown in examples 1 and 2 under the Partial Isotopomer specification above. 

# Question 11:
(b)
Text "Current InChI Isotopomer Specification ... <hydrogen_isotope_count> - number of the specified hydrogen isotope bonded to the designated atom (<atom_number>)" should be corrected as: "... <hydrogen_isotope_count> - number of the specified hydrogen isotope bonded to the designated atom (<atom_number>), 1 if omitted" 

Consequently, all the example InChI strings containing "...D1" or so should be corrected.

`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1/i1D1`
should be
`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1/i1D`

`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1/i7D1,8D1,9D1,10D1,11D1`
should be
`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1/i7D,8D,9D,10D,11D`
etc.

# *Answer*:
Thanks for bringing this to our attention.  We have fixed this error in the proposed isotopologue specifications above.

# Question 12:
It looks like my previous explanations have not reached their goal. So, below are more of them.

(1) On #4:

Complaining that it is not easy to understand InChI string or manually convert InChI into a structure should be  irrelevant to the InChI-related project: InChI is supposed to be understood either by software, or by experts, who feel comfortable with it. (this refers to words “ this is not easy to tell from the example without knowing the atom numbering and structure […]”)

# *Answer*:
We agree.  The partial isotopologue can be determined from the InChI itself.  Therefore, we have removed the commentary about not being easy to discern.  

# Question 13:
(2) I disagree with #5:

The canonicalization algorithm generates InChI, not molfile (this refers to words “the canonicalization algorithm will generate two identical MOL/SDF files for the two possible stereospecific configurations”)

To generate two stereospecific molfiles out of two stereospecific InChIs one needs to have these InChI. These two InChI are:

`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/i1D/t1-,2+,3+,4-,5+,6-/m0`
`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/i1D/t1-,2-,3-,4+,5-,6+`

Since these InChIs have not been mentioned in the write-up, it is not clear how the molfiles were supposed to be generated  (this refers to words “One problem is that it is not easy to generate a stereospecific MOL/SDF representation” and “the canonicalization algorithm will generate two identical MOL/SDF files for the two possible stereospecific configurations” )

A stereospecific molfile may easily be created by any comprehensive chemical structure editor: ACD/ChemSketch, ChemBioDraw, etc. It may be drawn  manually or created out of InChI since these editors use libinchi.dll/libinchi.so for InChI to structure conversion. (this paragraph refers to words “One problem is that it is not easy to generate a stereospecific MOL/SDF representation”)

InChI Trust software (libinchi.dll/libinchi.so) generates chemical structure connectivity with stereo parities out of InChI. This information is similar to stereo-SMILES and is sufficient  for producing a stereospecific molfile by chemical structure editors supporting InChI to structure conversion.  I guess, this fact is not known to the authors of the write-up, who used a buggy version of OpenBabel software for accessing this functionality of libinchi.dll/libinchi.so.

Producing molfiles with coordinates out of InChI was deliberately left out of the InChI Trust software functionality as well as, for instance,  evaluation of E-Z or S-R transition barriers or pKa values.

Instead of complaining about this deliberately missing functionality one might have used the working software,  not the buggy one.

(This section refers to words “The InChI Trust software does not create a stereospecific MOL/SDF file”).

Using OpenBabel for InChI to structure conversion was  a wrong choice of software by the authors of the write-up. I do not think sharing this experience in the text is a good idea for at least two reasons: (i) The text may be still available after OpenBabel has fixed the bug, thus making the text factually incorrect; (ii) The preferred way to encourage bug fixing is reporting  the bug to the OpenBabel  team instead of using project documentation as a platform  for publicly announcing  a bug in free and open-source software . (this refers to words “openbabel’s “--gen3D” option generates a segmentation fault when trying to convert from InChI to MOL/SDF format”)

# *Answer*:
Based on these suggestions, we have revised the description of example #5.  With the questions and issues being posed and more extensive discussions with the developers of the InChI Trust software, we are gaining a better understanding of the methods and use-cases driving the software implementation of the InChI standard. Also, we have posted issues on the OpenBabel github repository for the bugs we have discovered so far in that software.  We were just trying to provide a concrete example demonstrating some difficulty in generating stereospecific MOL/SDF representations.  But it is a good suggestion not to use momentary software bugs to make this point. The main point we are trying to highlight is that there is a growing use-case for the stereospecific interconversion between InChI and MOL/SDF.  However, the isotopologue specification proposal is probably not the correct venue for this discussion.  Therefore, we have revised the following commentary, but removed it from example #5:
 
One issue is that it is not easy to generate a stereospecific MOL/SDF representation.  The InChI Trust software does not create a stereospecific MOL/SDF file and its MOL/SDF conversion algorithm will generate two identical MOL/SDF files for the following two possible stereospecific configurations:

`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/i1D/t1-,2-,3-,4+,5-,6+`{: style="color: red; opacity: 0.80;" }
`InChI=1S/C6H12O6/c7-1-2-3(8)4(9)5(10)6(11)12-2/h2-11H,1H2/t2-,3-,4+,5-,6+/m1/s1`{: style="color: black; opacity: 0.80;" }`/i1D/t1-,2+,3+,4-,5+,6-/m0`{: style="color: red; opacity: 0.80;" }

In all fairness, generation of stereospecific MOL/SDF is not a use-case for the InChI Trust software.   Therefore, this use-case is de facto delegated to third-party software.

The growing importance of this stereospecific conversion use-case on use of molecular analytical data in a range of next-generation systems-level mathematical modeling of chemical and biochemical systems cannot be overstated.
