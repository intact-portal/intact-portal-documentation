# 5. Interaction level

After adding an experiment, you can add interactions using the Interaction tab on the Experiment page. These interactions will be created primarily attached to the experiment it was created under, however, the experiment that the interaction is attached to can be changed later, if needed. Each interaction is linked to a single experiment \(if an interaction is linked to several experiments – this is an error\).

The interaction page records the information about an interaction and the various factors that have an effect on the interaction.

Many interactions may be linked to a single experiment if they are all using the same experimental techniques. If a particular interaction is demonstrated several times in the same publication using the same experimental technique it need only be entered once, with all instances listed in the figure legend. Whenever there is a change in any one of host organism, interaction detection method or participant detection method, a new experiment must be created, even if the same interaction has already been demonstrated in the publication. Slight variations in the use of agonists/antagonists/ knock-out cell lines do not necessitate making a new interaction.

Interactions should be entered as binary interactions or n-ary interactions, as demonstrated within the specific experiment. All the interactions within a publication should be entered if possible, including positive controls. However it may not always be possible to enter all interactions in a paper, for a variety of reasons – see Table below:-

Unidentifiable interactors should be listed under the annotation “Data-Processing” \(please refer to this topic for further details\)

| **Common Reasons Why Interactions Cannot be Curated** |
| :--- |
| A participant\(s\) has only been partially identified e.g. ”actin”, “myosin”, PKA/C, AKT, Histone \(type 1/2/3\) |
| A “pan” antibody has been used, for example to multiple closely related antibody targets:-“ERK” “RAS” |
| Antibodies to Histones type H1/2/3 used – many of these antibodies cross-react with a variety of histone proteins or modified histones. This is often a problem with Ch-IP assays \(beware antibodies to H3K4me1/2/3\) |
| A significant proportion of the interactors cannot be unambiguously identified |

## 5.1 Interaction AC

An IntAct accession number is automatically assigned to each of the interaction, components, interactors, features, cross-references and annotations.

## 5.2 Short Label

The usual rules for Short Label apply. The interaction short label is automatically generated, based on any two gene names within the interaction \(bait is always first in a bait/prey relationship\) – but can be subsequently over-ridden so as to more accurately represent the interaction taking place. The short label is NOT a stable identifier for an interaction as it can change after any modifications.

## 5.3 Parameters

Parameters on interactions can act as holding places for kinetic values and values for physical properties of interactions, such as the Kd \(see [www.ebi.ac.uk/intact/interaction/EBI-9873160](http://www.ebi.ac.uk/intact/interaction/EBI-9873160)\). The unit used for Kd data should always be Molar \(M\). Additional information about the kinetics value described in parameters, or kinetic values which not on the parameter list should be added in annotation topic ‘kinetics’. The experimental conditions under which a kinetic parameter has been generated \(temp, pH\) should be entered under the annotation topic ‘kinetic\_conditions’ In cases where one or more mutant have an effect on the kinetics and either decreases or increases the rate of the reaction, the mutant\(s\) should be annotated at the features level for the protein as feature type “rate increasing/decreasing”. The corresponding parameter can then be added to this feature.

Only ONE value per parameter entry should be added at the Interaction level, which should always been the wild-type \(when given\). Additional values of, for example, Kds obtained using multiple different mutations of one protein can be entered onto the associated Feature for each mutation or as a “Comment”, if this is not possible.

However multiple \(different\) parameters can be added at the Interaction level.

## 5.4 Interaction type

The interaction type defines the type of interaction the molecules make, as demonstrated in each specific interaction.

Commonly used examples: association, physical association, direct interaction, colocalization.

This is a mandatory field.

### 5.4.1 Association

An association is an interaction in which more than one n-ary complexes are represented, assuming complexes as groups of molecules that are physically associated together at the same point. As a rule of thumb, any interaction with the Interaction Detection Method = affinity chromatography or one of its children \(e.g. coimmunoprecipitation, pulldown, TAP\) with 1 bait and MORE THAN 1 prey should be mapped to association, since more than one protein complex could be represented in the interaction.

No other experimental data has interaction type = association.

### 5.4.2 Physical Association

Any interaction in which the participants form a single n-ary complex \(identified with techniques that can ascertain that only one complex is present, like x-ray crystallography\), or a binary complex which may involve more interactors than those identified in the experiment should be described as ‘Physical Association’. Any interaction with the Interaction Detection Method = ‘affinity chromatography’ or one of their children \(e.g. coimmunoprecipitation, pulldown, TAP\) with one bait and only ONE prey should be mapped to ‘Physical Association’ \(unless the interaction occurs in vitro and consists of only 2 highly purified proteins in which case they should be mapped to ‘direct interaction’ \(see below\).

Examples:

In vivo IP with 1 bait and 1 prey

Yeast-2-hybrid assay

n-ary crystal

n-ary gel filtration

### 5.4.3 Direct Interaction

“Direct interaction” should only be used when there is no possibility of a third, unseen or ancillary molecule acting as a bridge between the two molecules of interest \(known small molecules bridging much larger molecules are an exception to this rule\).

NB: NO interaction occurring “in vivo” – in a cell or cell lysate – can be called “direct”.

An interaction should ONLY be described as direct if:

a. the number of interactors exactly equals 2 highly purified molecules \(plus optional small molecule\), or a homomultimer and

b. the host organism is "in vitro".

The "Experimental Detection Method" may be one of many types – most commonly biophysical methods such as X-Ray crystallography, enzyme assay or affinity chromatography methods.

### 5.4.4 Self or Putative Self Interaction

These are only used if 2 regions \(each purified separately\) of the same protein are interacting in vitro but it is unclear if this is an intra- or inter-molecular interaction. The molecule should be entered twice, with stoichiometry=0. The interaction type and experimental role ‘self/putative self’ will then be used. The interaction types self interaction/putative self-interaction should NOT be used for autocatalysis, when the additional biological role ‘self/putative self’ will supply this information.

### 5.4.5 Colocalization

Experiments which describe the purification of complexes where interactors may not interact \(e.g. cosedimentation\) or imaging studies \(e.g. confocal/fluorescence microscopy\) where it is difficult to assess if the interactors have a physical association must have the interaction type set to colocalization.

Gold immunostaining data \(using Electron density methods/ electron microscopy\) is acceptable as co-localization data when there is a clear distinction between the labelled particles, usually on the basis of size.

Colocalization between molecules will be captured only when, within the same paper, there is a physical interaction evidence.

Colocalizations where one of the proteins is only used because it is an indicator of a particular subcellular location, are NOT captured.

\*\* Where the interactors co-occur in the same subcellular compartment these can also be annotated using the interaction type: colocalization and the appropriate GO term for the subcellular location of the colocalisation be entered as an Xref.

5.5 Causal Interaction annotation \(NA-MIMIX\)

* See end of the document

## 5.5 Interaction Annotations \(NA-MIMIX except Figure legends\)

Any publicly available specific instances of “Interaction annotation” can be searched for in the public database using the “advanced\_search”, selecting for the field “Interaction annotation” and entering the specific term needed e.g. “isoform-comment”.

### 5.5.1 Commonly used Interaction Annotations

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Annotation</b>
      </th>
      <th style="text-align:left"><b>Definition/Comments</b>
      </th>
      <th style="text-align:left"><b>Examples</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">antagonist</td>
      <td style="text-align:left">Any molecule applied externally to cells or any type of environmental
        condition, such as hypoxia, that inhibits an interaction, potentially by
        alteration of amount or binding affinity of one or more of the interactors.</td>
      <td
      style="text-align:left">
        <p>EBI-6397393: Neratinib, an irreversible inhibitor of EGFR/HER kinases.</p>
        <p>EBI-2879898: SB216763 - a GSK-3 inhibitor.</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">agonist</td>
      <td style="text-align:left">
        <p>Any molecule applied externally to cells or any type of environmental
          condition, such as hypoxia, that stimulates an interaction, potentially
          by causing modification of one or more of the interactors.</p>
        <p>[Further description of the agonist should be included, if necessary]</p>
      </td>
      <td style="text-align:left">
        <p>EBI-6397393: PD0325901 &#x2013; A MEK inhibitor.</p>
        <p>EBI-6395914: Amino acid starvation.</p>
        <p>EBI-6127767: Thapsigargin (an irreversible sarcoplasmic/endoplasmic reticulum
          Ca2+-ATPase)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>3d-structure</p>
        <p>3d-r-factor</p>
        <p>3d-resolution</p>
      </td>
      <td style="text-align:left">These terms are used in the curation of crystallographic data &#x2013;
        see later</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">aomment</td>
      <td style="text-align:left">Add any info here that cannot be adequately described under any other
        type of annotation category</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">inhibitor</td>
      <td style="text-align:left">Use to capture information on the action of a molecule which is directly
        inhibiting an interaction but you do not feel appropriate to add as an
        interactor. Usually only used with purified proteins where the inhibited
        interactor can be identified.</td>
      <td style="text-align:left">
        <p>EBI-447320: This interaction was disrupted by chetomin</p>
        <p>EBI-447720 - Inhibition by autophosphorylation of IRAK-1 at undefined
          position(s).</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">kinetics</td>
      <td style="text-align:left">Use to capture additional kinetic data (such as effect of a mutation or
        a kinetic value not available as a Parameter). The units used should always
        be stated, and must be applicable to the kinetic value being given. Use
        SI units wherever possible.</td>
      <td style="text-align:left">
        <p>EBI-591030: The affinity between TGN38 cytoplasmic tail and the mutant
          Y350A adaptin mu2 mutant is kd = 7.55 10-7 M</p>
        <p>EBI-519455: FIST protein which had a truncated kinase domain (142- 433)
          displayed reduced binding affinity for Daxx in this study.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">resulting-ptm</td>
      <td style="text-align:left">Previously used to records the addition of a PTM on a participant as the
        result of an enzymatic reaction or child thereof. This should now be added
        as a feature role</td>
      <td style="text-align:left">
        <p>EBI-2941958: Tyrosine phosphorylation of EGFR</p>
        <p>EBI-4479606: Sirt1 reduced the acetylation level of GST-c-Myc in the presence
          of NAD+.</p>
        <p>EBI-3890310: mono-methylation of RelA (Lys310me1).</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">stimulant</td>
      <td style="text-align:left">Use to capture information on the action of a molecule which is directly
        stimulating an interaction but you do not feel appropriate to add as an
        interactor. Usually only used with purified proteins where the stimulated
        interactor can be identified.</td>
      <td style="text-align:left">EBI-515302 Cross-linking of GPIV (Q9UIF2) in platelets increased associated
        FcR gamma chain (P30273).</td>
    </tr>
  </tbody>
</table>

The annotation comments Complex-properties, Curated complexes and Complex synonyms are only used for the curation of curated complexes and should not be used for experimental interaction evidence curation.

### 5.5.2 figure-legend \(MIMIX applicable\)

This is the figure number in the paper where the interaction was shown. It is however essential that this be added where available.

Examples:

figure-legend: 1

figure-legend: 2a and 2b

A Figure-legend need NOT be added for screening data such as two hybrid or mass spectrometry, if none is given in the publication.

If the data is \(also\) given in a table, enter the table number instead of or in addition to the figure legend.

### 5.5.3 negative

This must be added on the entries made for negative interactions. See section 4.6.9 for usage.

### 5.5.4 uniprot-cc-note

This annotation is added to specify the text which is exported into UniProtKB as a "note" in the CC INTERACTION block. This is not currently exported for public viewing. Notes should be added using Swiss-Prot syntax.

### 5.5.5 url

The url of an external database from which the interaction data originated. This is generally only added to submitted data at the request of the submitter.

| **Interaction AC** | **Description** |
| :--- | :--- |
| EBI-308790 | http://www.kazusa.or.jp/tech-cgi/tablelist.ppi.cgi |

### 5.5.6 3d Structural data

 **Crystals**

There are 3 extra Interaction annotations, ‘3d-resolution’, ‘3d-r-factors’ and ‘3d structure’. Add the PDB accession code e.g. ‘3S6N’ as xref, with the qualifier ‘Identity’. This can usually be found in the publication, or can be searched for on the PDB site using the PMID.

The PDBe web site can be found at: [http://www.ebi.ac.uk/pdbe/](http://www.ebi.ac.uk/pdbe/)

Experimental roles are “Neutral” for crystals. Host Organism: ‘in vitro’ – \(with “expressed-in” for participants\).

Many details regarding the interaction can be found in the relevant PDBe entry, notably R Factors, resolution, mapping to UniProt, sequence numbering, presence of ligands etc. Binding regions can be LINKED.

Stoichiometry can be found under “Structure analysis”

“Assembly composition” was included in the PDBe import but is generally not added to manually curated entries.

Example entry:-

![](../../.gitbook/assets/0%20%284%29.png)

#### 6.5.5.1 3d structure

This annotation topic can be used to comment on the structure of the 3D-complex but is optional.

#### 6.5.5.2 3d-r-factor

This annotation topic should be used to denote the r-factor of the structure.

| **Interaction AC** | **Description** |
| :--- | :--- |
| EBI-297231 | working 19.1%, free 20.6% |
| EBI-539447 | working 25.0%, free 29.6% |

#### 6.5.5.3 3d-resolution

This annotation topic should be used in conjunction with crystallographic data to denote the resolution of the structure. Units in angstrom \(A\) should be used; the text field however does not allow the entry of the superscript hence enter it as shown in the Table.

| **Interaction AC** | **Description** |
| :--- | :--- |
| EBI-449117 | 1.46A |

### 5.5.6 variable\_condition\_1/2

Describes the parameter varied throughout a set of interactions and should only be used when the annotation topic 4.6.11 “variable” has been added onto the associated **experiment**. Example: EBI-1255485.

## 5.6 Cross-references and cross-reference qualifiers

All added Cross references must have a qualifier: For the GO database the qualifier is added automatically, others must be entered manually.

A GO annotation\(s\) is normally added for the cellular location of an interaction for co-localisation experiments. For non-co-localisation experiments it can be added when an interactions occurs in a particular **CELLULAR COMPARTMENT**_,_ e.g. nucleus.

A PDB cross reference is always added for crystals.

**Note:** References relating to the **protein** should be added on the **Participant** level using the Feature editor \(e.g. InterPro Cross-Reference\);

**Databases: Qualifiers**

pubmed: see-also

go: e.g. component, process, function

pdb: identity, see-also

intact: see-also, intact-secondary

reactome identity, see-also

omim: see-also

intenz: identity

### 5.6.1 identity

This cross-reference qualifier should be used when the cross-reference describes an equivalent entry in another database. Example: For a PDB entry, the database is ‘wwpdb’, the ID is ‘PDB AC’ and the cross-reference qualifier is ‘identity’.

Example: [EBI-297231](http://www.ebi.ac.uk/intact/search/do/search?searchString=EBI-297231)

### 5.6.2 see-also

This cross-reference qualifier should be used when there is additional information in another IntAct entry or external database which would add value to this entry for the user. For example, there may be information in a second publication which is not captured here but is relevant to the entry, in which case the PubMed xref should be given the qualifier ‘see-also’.

When the same interaction is described in other databases but not in as much detail, cross-reference with the qualifier see-also.

### 5.6.3 GO cross-references

GO xrefs are added at the interaction level to give additional information about the subcellular location where an interaction occurs, and on enzyme assays to indicate the function and process demonstrated by that assay. The qualifier need not be added – that is added automatically on hitting Save. Under some circumstances the qualifier is not imported correctly or not imported at all and may need to be changed manually. Please always check the accuracy of the qualifier after saving.

If a required term is not available please request the term at:

[https://github.com/geneontology/go-ontology/issues](https://github.com/geneontology/go-ontology/issues)

### 5.6.4 intact-secondary

intact-secondary will be used as a qualifier on accession numbers associated with withdrawn interactions that have been remapped.

