# 7. Participant feature

A feature is added on the participant to more fully describe the construct used in the experiment and will contain information such as binding region, mutation or deletions, tags.

On submitting the features, these will be visible on the interaction page. Linking of the features will have to be carried out from the interaction page.

Example of a simple feature:

![](../../.gitbook/assets/0%20%287%29.png)

A more unusual feature:

![](../../.gitbook/assets/1%20%285%29.png)

A Feature with “Fuzzy” type range: the authors have not given the range for the interacting region, so this has been deduced \(generally from UniProt Sequence Annotation\):

## 7.1 Fields required to describe a Feature

<table>
  <thead>
    <tr>
      <th style="text-align:left">Short label (obligatory)</th>
      <th style="text-align:left">This does not auto-generate. It may be based on the InterPro name of a
        feature e.g. SH3 domain. The default term &#x201C;region&#x201D; is used
        if no more informative term can be found. Mutations are a special case,
        as described in section 7.3.5.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Feature Type (obligatory)</td>
      <td style="text-align:left">Use the most appropriate CV term to describe the feature or modification</td>
    </tr>
    <tr>
      <td style="text-align:left">Detection Method (optional)</td>
      <td style="text-align:left">e.g. deletion analysis</td>
    </tr>
    <tr>
      <td style="text-align:left">Range (obligatory)</td>
      <td style="text-align:left">
        <p>Ranges can be specific or indeterminate and describe the position of the
          feature within the sequence of the molecule.</p>
        <p>A feature may have MORE than one Range.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">X-Refs</td>
      <td style="text-align:left">When a range binding site feature can be matched to an InterPro domain,
        enter InterPro Xrefs at the feature level: these can be found from the
        UniProt entry page under Cross References/InterPro/ Graphical view. The
        IPR number is entered with qualifier &#x201C;identity&#x201D; (Example
        IPR000001 for Kringle)</td>
    </tr>
  </tbody>
</table>

## 7.2 Examples of various features

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Feature type</b>
      </th>
      <th style="text-align:left"><b>Feature AC</b>
      </th>
      <th style="text-align:left"><b>Short Label</b>
      </th>
      <th style="text-align:left"><b>Range</b>
      </th>
      <th style="text-align:left"><b>Feature detection</b>
      </th>
      <th style="text-align:left"><b>Xref (qualifier)</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">required to bind</td>
      <td style="text-align:left">EBI-6128250</td>
      <td style="text-align:left">region</td>
      <td style="text-align:left">51-372</td>
      <td style="text-align:left">deletion analysis</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">sufficient to bind</td>
      <td style="text-align:left">EBI-4373855</td>
      <td style="text-align:left">fadd-dd</td>
      <td style="text-align:left">93-191</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">
        <p>IPR011029</p>
        <p>(identity)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">mutation decreasing</td>
      <td style="text-align:left">EBI-9212561</td>
      <td style="text-align:left">p.Tyr39Phe</td>
      <td style="text-align:left">39-39</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">opthr (Phosphothreonine)</td>
      <td style="text-align:left">EBI-6162530</td>
      <td style="text-align:left">thr-33</td>
      <td style="text-align:left">33-33</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">-</td>
    </tr>
    <tr>
      <td style="text-align:left">35s radiolabelled</td>
      <td style="text-align:left">EBI-2911435</td>
      <td style="text-align:left">region</td>
      <td style="text-align:left">?-?</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">-</td>
    </tr>
    <tr>
      <td style="text-align:left">flag tagged</td>
      <td style="text-align:left">EBI-2616889</td>
      <td style="text-align:left">n-terminus</td>
      <td style="text-align:left">n-n</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">-</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>tagged molecule</p>
        <p>(non-standard tags)</p>
      </td>
      <td style="text-align:left">
        <p>EBI-6270838</p>
        <p>EBI-6250853</p>
        <p>EBI-4370535</p>
      </td>
      <td style="text-align:left">
        <p>sumo tag</p>
        <p>halo_biotin_tag</p>
        <p>s-peptide tag</p>
      </td>
      <td style="text-align:left">
        <p>?-?</p>
        <p>c-c</p>
        <p>n-n</p>
      </td>
      <td style="text-align:left">-</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

**Note:** binding site has two children, ‘sufficient to bind’ \(binding observed with construct shorter than full-length molecule\) and ‘required to bind’ \(binding not observed with region deleted from full-length construct.

If amino acids are sequentially mutated to alanine, the feature detection method is alanine scanning.

**Features** can also be added to nucleic acids and genes. Gene features are currently not mapped to sequence, use range= ?-?

**Some examples of Nucleic Acid Features**

| **Short label** | **CV term** |
| :--- | :--- |
| promoter\_region | Binding region |
| tp53 response element region | Binding region |
| hypoxia\_response\_element\_promoter\_region | Binding region |
| promoter\_cpg\_island | Binding region |
| promoter vdre \(vitamin d response element\) | Binding region |
| transcription start site | Binding region |

**Feature Type:  RNA chemical modification id MI:2202**

for Ribonucleotide modifications \(such as methylation, pseudouridylation etc.**\)**. The specific modification is then indicated as an Xref with database = ChEBI.

**Example:** [_N\(6\)_](https://www.ebi.ac.uk/chebi/searchId.do?chebiId=CHEBI:21891)[-methyladenosine](https://www.ebi.ac.uk/chebi/searchId.do?chebiId=CHEBI:21891): CHEBI:21891

A useful Database for RNA Mods:-http://mods.rna.albany.edu/mods/

Also http://modomics.genesilico.pl/modifications/

**Feature Type:  DNA chemical modification, id: MI:2201**

**Example:** [5-methyl-2'-deoxycytidine:](https://www.ebi.ac.uk/chebi/searchId.do?chebiId=CHEBI:47876) CHEBI**:**47876 \(as an Xref\).

For both, RNA and DNA modifications, the full name of the mod - e.g. "N6-methyladenosine" can be added as the short-label.

## 7.3 Specific cases

The Feature Editor should be used in the following cases:

### 7.3.1 Molecule is tagged

The term “Tag” includes small peptide i.e. “epitope-tags” e.g. Flag, V5 and also larger fusion proteins e.g. GFP, GST.

Curators need **not** enter feature type ‘tag’ or children of this term where the Interaction detection method is a standard ‘protein complementation assay’ or a child term AND the tag is explained in the definition of the method used or is used regularly with the method.

For example Interaction Detection Methods such as:-

Two Hybrid, DHFR reconstruction, Luciferase Complementation assay.

If, however, the tag is non-standard this DOES need to be added.

Short Label

The short label is used to describe the position of the tag i.e. ‘’ or ‘n-terminus’-when this information is available.

N.B. The term “terminus” is used to show the location of a TAG, whereas the term “terminal” is used to describe the location of a protein sequence.

If the position of the tag is known specific amino-acid positions should be entered. If the position is not known, the range ‘?-?’ is added. If a novel or non-standard tag is used, i.e. one not present in the current controlled vocabularies, the short label will give this information so- ‘xyz-tag n-terminus’ with Feature type ‘tag’. \(see examples in Table above\)

If the protein has multiple tags, they should be entered as separated features.

Examples:

EBI-6250852 – both a His and V5 tag

EBI-4370371 – both an s-peptide and His tag

### 7.3.2 Molecule is radio-labelled

Short Label – This is usually “region”, unless a specific residue/region is known to be labelled, in which case this residue or region should be entered in the short label, e.g. “arg-15” or “n-terminus”.

Feature Type: Choose the exact “radio-label” used from the drop down list; example 131i radiolabel or 35s radiolabel

Range - The actual position of the radio-labelling, if specifically known, should be entered in the range – using amino acid positions. Otherwise, Range will be ‘?-?’ if the position is unknown or the protein was globally labelled.

Example: Protein expressed in bacteria grown in 35S growth medium

EBI-465724.

### 7.3.3 Molecule is post-translationally modified \(PTM\)

Each individual PTM goes in as a separate feature.

The Short Label of the PTM should include the term ‘\(possible\)’ or ‘\(required\)’:- ‘\(possible\)’ will be used where the authors have used a protein with a PTM but have not shown that the interaction depends on the PTM. For example: phosphorylated Protein A has been shown to interact with Protein B but no-one has shown that the dephosphorylated form does not. Do not list all “possible” PTMs present in a UniProtKB entry – only those discussed in the paper. Only in cases where the authors have shown in the paper being annotated that the PTM is necessary for the interaction should ‘\(required\)’ be used.

Feature Type – select the appropriate term from PSI-MOD \(the Ontology can be found in OLS under “**Protein Modifications’** \([http://www.ebi.ac.uk/ontology-lookup/browse.do?ontName=MOD](http://www.ebi.ac.uk/ontology-lookup/browse.do?ontName=MOD)\) OR after March 2016:

http://www.ebi.ac.uk/ols/ ontologies/mod

and find the matching “Short label curated by PSI-MOD synonym” in the Editor feature drop-down menu.

e.g.

Editor short label: possible phosphoser-129

Feature Type: “opser” \(O-phosphorylated L-serine\) \(from PSI-MOD short label\)

Range 129-129

Editor short label: lys-123

Feature Type: ”NacLys” \(N-acetylated-lysine\)

Range 123-123

If Range is _unknown_ enter ?-?

‘Feature detection method’ may also be entered, if described in the paper.

Commonly used Feature Detection Methods:

‘deletion analysis’, ‘mutational analysis’

**Note** – if a PTM is produced as a RESULT of the interaction that you are annotating, this is **not** a feature of the molecules but a “Resulting PTM” which is an annotation topic.

EBI-2941958 \(resulting PTM: Tyrosine phosphorylation of EGFR\)

Special case: Ubiquitin. This small protein can be linked to another protein as a PTM –ubiquitination. Alternatively, it can be entered as a protein participating in an interaction. As Ubiquitin can be derived from multiple genes, and the exact source is often unknown, entering as the IntAct internal protein ubiq\_human, ubiq\_mouse, ubiq\_arath etc. circumvents the need to know this. Calmodulin is also derived from 3 genes \(human\) and Histone H4 from 1 but these have not yet been demerged into separate entries by UniProtKB/Swiss-Prot.

Identical proteins may be added as protein sets.

Sumoylation, neddylation, myristoylation, farnesylation, glycosylphosphatidylinositol \(GPI\) anchor formation, pupylation and ISGylation result in PTMs formed by the addition of a peptide/small protein or a hydrophobic group.

We do NOT enter the formation of PTMs as interactions, e.g. the ubiquitination of proteins, unless these are described as isolated enzyme assays. Intracellular ubiquitination, for example, is not added.

### 7.3.4 Molecule is a fragment, truncation or deletion construct

If a paper describes a series of deletion constructs, annotate to the **shortest region** that interacts. It is NOT necessary to list each separate deletion mutant used by an author. Deletion mutations should be described as featureType = “required to bind” or “sufficient to bind” where possible.

For Example: Protein A \(length 50aa\) binds to Protein B. A deletion mutant of Protein A is constructed from regions 1-20 and 30-50 and this fails to bind. Annotate the fragment 21-29 as the ‘**required to bind**_’_ with feature detection as ‘deletion analysis’.

Example: EBI-465428

**Short Label**: This may be described just as ‘region’ or the Short Label may be used to give a more detailed description or features within the fragment Example: ‘sh3 domain’, ‘heat repeat’, ‘nad’ \(for NAD-binding site\), where the fragment contains the domain, repeat or binding site respectively.

For C-terminal fragments, the Short Label will be ‘c-terminal’

For N-terminal fragments, the Short Label will be ‘n-terminal’

For the cytoplasmic region, the Short Label will be ‘cytoplasmic region’

For transmembrane fragments, Short Label will be ‘transmembrane region’

Example: EBI-77516

Where an InterPro domain, repeat or binding site has been defined, the Short Label can be derived from the names of these domains. Example: ‘sh3 domain’, ‘heat repeat’, ‘nad’ \(for NAD-binding site\). Use the InterPro short name if the InterPro domain name exceeds 256 characters.

**FeatureType** = ‘binding site’ \(this does not imply all domains within a fragment are necessarily involved in binding\). Children of this term – ‘required to bind’ and ‘sufficient to bind’ – should be used where possible.

**Range** – range defines the binding fragment of the protein.

**Cross-reference** - if this binding site has a domain, repeat, well defined binding site or active site relevant to the interaction, this should be added in as a cross-reference with the database = ‘interpro’, primary id = ‘InterPro accession number’ and qualifier = ‘identity’. Example: EBI-457906

### 7.3.5 Molecule contains a Mutation

There are many different varieties of “mutations”, some of which are naturally occurring, however ‘mutation’ in the PSI-MI CV refers to an artefactual change to a sequence, the term ‘variant’ is used for polymorphisms.

GENERAL POINTS regarding Mutations:

XML3.0 contains a defined field to describe the sequence change created by a point mutation and this **must always be filled in**. This is a defined field and can be added using the drop-down menu in the tabbed field ‘Sequence and resulting sequence’

XML2.5 lacks this field, we therefore use the **SHORT LABEL** to give the location of the original un-mutated amino acid\(s\) and the identity of both the original and resulting amino acid\(s\) produced by the mutation. Short label should be reported according to the [http://varnomen.hgvs.org/recommendations/protein](http://varnomen.hgvs.org/recommendations/protein). Examples and further development of the HGVS rules as applied in IntAct curation can be found here: [https://docs.google.com/document/d/1OTIv0ygFaU\_G4bAB0ej6TfbU7acjhMweNMLopMTA3bw/edit](https://docs.google.com/document/d/1OTIv0ygFaU_G4bAB0ej6TfbU7acjhMweNMLopMTA3bw/edit).

N.B. When entering the position of a mutation, as quoted in a publication, it is advisable to check in UniProt that the relevant amino acid\(s\) really ARE at the position quoted, for the appropriate species. If not, remap to the correct positions.

If the experiment used both, a wild type fragment and a mutated fragment:

* if the mutation impairs/increases an interaction, it should be entered on the positive interaction with a Feature type “mutation decreasing/increasing” etc...
* if the mutation does not change the interaction: please curate as ‘mutation with no effect’.
* if the mutation changes the kinetics \(e.g. as in mutations of an enzyme\), it should be ‘mutation increasing/decreasing the rate of an interaction’

Mutations that are **not** in the same construct i.e. a series of point mutations have been made, that have **separately** been shown to have an effect, these should be individually entered as a separate feature for each mutation on the same interaction. However, if the effect has only been shown when mutations have **all** been made within the same instance of the molecule i.e. several mutations **in the same construct**, this should be described as a single feature.

**Rules for mutation increasing/decreasing short label notation**:

Please see [http://varnomen.hgvs.org/recommendations](http://varnomen.hgvs.org/recommendations) and [https://docs.google.com/document/d/1OTIv0ygFaU\_G4bAB0ej6TfbU7acjhMweNMLopMTA3bw/edit](https://docs.google.com/document/d/1OTIv0ygFaU_G4bAB0ej6TfbU7acjhMweNMLopMTA3bw/edit).

If an interaction contains molecules with multiple mutations and it is not clear what the combined effects of the mutations are, a Comment \(preferably taken from the text\) can be entered instead of multiple individual mutations.

**Unusual feature: Polyglutamine Tract/Repeat:**

The exact content of the PolyG tract can be described in ‘Sequence and resulting sequence’ by adding the appropriate number of Gln molecules.

![](../../.gitbook/assets/2.png)

**Example of a mutated bait with differing effects on multiple prey**

There are 3 Interactions with **3** different baits – WT, Mutant X and Mutant Y

| **Bait A** | **Wild Type** | **Mutant X** | **Mutant Y** |
| :--- | :--- | :--- | :--- |
| Prey B | + | + |  |
| Prey C | + |  |  |
| Prey D | + | + | + |
| Prey E | + | + |  |

Each different Bait molecule is entered as a separate interaction:

Wild Type Bait interacts with ALL Prey proteins.

Mutant X Bait X - amino acid change should be added as a feature to Bait A as ‘mutation’ as X interacts with Preys B, D and E.

Mutant Y Bait Y - amino acid change should be added as a feature to Bait A as ‘mutation’ as Y only interacts with Prey D.

### 7.3.6 Linking features

An experiment may show specific residues within two proteins interact, or a residue on Protein A interacts with a domain on Protein B.

For example, domain 50-100 on protein A has been shown to interact with domain 200-250 of protein B

Protein A will have feature Short Label ‘region’, feature type ‘sufficient to bind’ range ’50-100’

Protein B will have feature Short Label **‘**region**’**, feature type ‘sufficient to bind’ range ‘200-250’.

The above features should be linked if they interact, using the ‘Link Feature’ button on the Interaction page. Select the relevant features using the checkboxes next to each Feature, then press ‘Link Feature’. Domains must be shown to interact in the same interaction, and should be precisely defined – a fragment of unknown coordinates should not be linked.

If one domain “A”, from protein X is shown interacting with full length Protein Z in one interaction, and domain B from Protein Z interacts with full length Protein X, they should not be linked if there is no direct evidence that domain A binds to domain B.

Some examples where Features should be linked are:

* one amino acid of one of the proteins is shown to interact with an amino acid of another
* Phosphorylated amino acid is shown to interact with a SH2 domain
* When PTM\(s\) on proteins are important or necessary for the interaction, these should be linked to the interacting region.

Features within a participant in an interaction may be linked to each other. Example: Interaction: EBI-519830, Features EBI-540445 and EBI-540447 are linked and interacting.

### 7.3.7 Fusion proteins/unusual Tags

\(See earlier section for Identification of naturally occurring fusion proteins e.g. BCR-ABL\)

If a tag or fusion protein is not on the drop-down menu, ‘Create a Feature’ on the protein. Add Short label: e.g. “xanadu protein” \(using the name of the tag or protein fused\)

Feature type: tag or fusion protein

As the Term ‘tag’ is a child of ‘fusion protein’, the term ‘fusion protein’ might be applicable to large tags, but only if the tag/fusion protein does not participate in the interaction or has NO biological properties. The tag protein may have been added to assist in isolation, identification of solubility of the protein to which it has been used.

In cases where a fusion protein or chimeric construct has biological properties and participates in the interaction, this data will normally not be curated. However, if there is a reason for doing so, then a new protein has to be created in the editor with the entire sequence of the fused proteins.

 7.4 Adding feature to a Complex as a participant

See:

[https://docs.google.com/document/d/1yDoHnxKi6JY16H3jq9l7A2VzEu01FNvyVFYSpsWZfeA/edit?usp=sharing](https://docs.google.com/document/d/1yDoHnxKi6JY16H3jq9l7A2VzEu01FNvyVFYSpsWZfeA/edit?usp=sharing)

7.5 GAGs

* If GAG is interactor: use new feature “carbohydrate chemical modification” and capture nature of modification in short label, xref to MOD if required.
* GAG as protein modification: New feature type “attached carbohydrate” with MOD as xref to the modification species and chemical modification in short label of feature
* Chemical modification on GAG affecting interaction: New feature type “attached carbohydrate affecting interaction” and a reference to WT that has feature type “attached carbohydrate”. Effects can be reported with appropriate children terms \(e.g. “attached carbohydrate increasing/decreasing interaction”\), in a similar way mutations are handled.

