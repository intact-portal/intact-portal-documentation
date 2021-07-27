# 6. Participant level

The **participant** defines the **interactor** construct when it enters an interaction.

Participant = Interactor + Features.

The feature imparts additional properties to the interactor.

Proteins, small molecules, nucleic acids, complexes and genes are currently interactors in IntAct.

##  6.1 Proteins

On entering a new UniProtKB AC \(Accession Number e.g. **P01308**\) into IntAct, a participant entry is created. Information such as the ID, UniProtKB entry name \(e.g. [INS\_HUMAN](http://www.uniprot.org/uniprot/P01308#section_general)\), Gene Name, Organism and sequence are imported directly from the UniProtKB entry. An Intact AC number is assigned to every interactor. The Intact AC number can also be used to retrieve a protein entry.

### 6.1.1 How to find a UniProt Identifier for your proteins

Proteins are preferentially mapped to UniProtKB/SwissProt entries. If no UniProtKB/SwissProt entry is available, the mapping is to the longest UniProtKB/TrEMBL entry. Searches are performed for UniProtKB IDs based on the gene or protein name, identifier, cross-references, accession numbers or sequence provided by the authors.

\(Hint - if the UniProt Database is down or slow, try replacing “www” in “[http://www.uniprot.org](http://www.uniprot.org/)” with “ebi”,“sib” or “pir”, for local access.\)

The “ID mapping” service at [https://www.uniprot.org/uploadlists/](https://www.uniprot.org/uploadlists/) can be available to obtain the UniProtKB identifiers should only non-UniProt identifiers be provided by authors \(note -proteins with GI numbers as identifiers can only be cross referenced if the “GI” prefix is removed\). Author given names which cannot be traced in UniProt can be added as an alias on the participant.

If your publication only provides exon info for your protein, find the Gene in Ensembl \(Cross-Refs\) and click on the appropriate TRANSCRIPT \(compare aa length\). Click on “PROTEIN link” at TOP LHS \(left hand side\) and this will give the amino acids from each exon in alternating colours. If necessary, you can blast the amino acid sequences to get the numerical range.

If the exact strain of the organism from which you protein of interest is missing, but there is a Reference Proteome for that species in UniProtKB, map to the Reference Proteome. To find the Reference Proteome, select the UniProt Taxonomy search menu and enter your organism e.g. [Staphylococcus aureus](http://www.uniprot.org/taxonomy/93061). Use the ‘Advanced Search’ to filter the result by ‘Reference Proteome \(yes/no\), and choose ‘yes’. This should be “strain NCTC 8325”, which has a TAX ID of 93061.

Proteins can be found for this organism by searching for the Name of your protein **and** the TaxID. E.g. “Nitroalkaneoxidase AND 93061” gives a UniProt ID of [Q2FZX9](http://www.uniprot.org/uniprot/Q2FZX9).

#### 6.1.1.1 Tracing the Species of origin of a protein

Where it is NOT immediately apparent from which species the protein has originated, the following steps can be taken

a. Reference chasing \(potentially going back many years\)

b. Curator writes to the author, and receives additional information \(or not\).

c. Curator takes sequence information from paper e.g. protein length, amino acid positions of mutants and unequivocally maps to a single entry in the protein sequence database.

d. Curator looks at previous work of author \(or group donating clone\) and only one species has previously been used. \(The Addgene \(non-profit\) repository has a large collection of donated plasmids, that names depositors, and it is worth checking at [http://www.addgene.org/](http://www.addgene.org/) if your author\(s\) has donated plasmids here.\)

In all cases, the decision tree used to assign a database accession number to the protein should be documented as a Data Processing comment.

#### 6.1.1.2 Identification of naturally occurring fusion proteins

Examples: BCL-ABL1, MLL/AF4etc**.**

Interactions involving this type of protein are commonly found in cancer related journals. The exact identity or sequence of the fusion protein\(s\) is rarely given by the authors. In this case choose a UniProt entry best representing the features you wish to show and add a Data-Processing comment to the effect:

The fusion protein "BCR-ABL" has been entered as TrEMBL entry A9UEZ6. This is a reference entry only and may not be an exact match to the sequence of the protein mentioned in this publication.

#### 6.1.1.3 Artificial fusion proteins

Interactions involving artificial chimeric/fusion proteins that are of NO biological relevance need NOT be curated, e.g. PMID: 22939624, chimeric kinase constructs in which one loop region/N-lobe was fused into another molecule – or domains reciprocally switched between molecules.

You may however choose to additionally annotate artefactual chimeric molecules when the sequence is available or can be reconstructed from the paper, but in most cases, this data will NOT be curated.

If an organism database or source database for the interactor identifier is not in the PSI CV and you need to cross-reference it, please request a term at the PSI-MI CV GitHub site by creating an issue \([https://github.com/HUPO-PSI/psi-mi-CV/issues](https://github.com/HUPO-PSI/psi-mi-CV/issues)\).

#### 6.1.1.4 Identifying a protein by sequence searching

Where only sequences are available, Blast should be used for protein and/or short peptide matching. The best match showing a 98% sequence identity \(or greater\) that extends over 98% of the query or matched sequence should be used for annotation.

If there is a database identifier with a sequence attached to it but NO UniProtKB entry can be found after ID mapping, carry out a blast sequence alignment. If no sequence is seen to match any UniProtKB entry create a new protein in the editor with a database cross reference, setting the database identifier qualifier to ‘Identity’. A Comment should be made as to the UniProtKB orthologue in the nearest related species to enable manual mapping in the future. The sequence must be entered.

If a published protein sequence cannot be traced to a UniProtKB entry, the sequence information can be deposited at

[http://www.ebi.ac.uk/swissprot/Submissions/spin/index.jsp](http://www.ebi.ac.uk/swissprot/Submissions/spin/index.jsp)

In the case of Mass Spec Data, contact email: [help@uniprot.org](mailto:help@uniprot.org)

Request for TrEMBL entries to be merged as isoforms into a UniProtKB?Swiss-Prot entry should be to [http://www.uniprot.org/update](http://www.uniprot.org/update)

If the protein is found only in UniParc, contact Sandra Orchard

\([Orchard](mailto:Orchard@ebi.ac.uk)[@ebi.ac.uk](mailto:Orchard@ebi.ac.uk)\)

When a protein cannot be assigned from information in the paper or references, the author should be contacted to supply the missing information. If there is no response after ~ two weeks, curate all possible interactions in the paper, and make a note of missing proteins under the heading “data-processing”. If the author contacts the database following release with the missing information the entry should be updated.

Where the peptide mapping by the author to the entries is problematic or the match of a mass spec peptide sequence to the identified protein is not 100 %, this information should be added to the data-processing and the interactions involving this protein should not be entered. This is one instance when there will be a discrepancy in the interaction numbers provided by the author and the ones in IntAct in a large-scale experiment.

### 6.1.2 Mapping of protein isoforms

If an author states that a specific isoform has been used or identified in an interaction, this information should be included. Should the isoform be identifiable within an entry the interaction should then be mapped to this UniProt AC, for example PMID:11517249 uses murine Jip1 isoform b which is described by Q9WVI9-1. If there is no attempt to identify a particular isoform, the parent/canonical UniProtKB AC should be used. If the authors list an isoform which cannot be identified from those currently described in the corresponding UniProtKB record, an "[isoform-comment]()" should be added as an annotation.

However, if a sequence is given for this isoform, which would indicate it is either a novel sequence, not already in UniProtKB/Swiss-Prot or the required sequence is in TrEMBL, contact [http://www.uniprot.org/update](http://www.uniprot.org/update) and request the isoform be added to the Swiss-Prot entry. If you curate to the TrEMBL entry, the isoform information will be lost when the entry is merged into Swiss-Prot as the interaction data is transferred to the canonical sequence. This will be particularly confusing if there are both positive and negative isoform interactions for the gene products.

Whilst waiting for the Swiss-Prot update, you may create the new isoform as an internal protein with a “no uniprot update” annotation - leave this annotation in place until the new isoform has been released \(from UniProt\) or the new isoform info will be lost on any IntAct protein update prior to that event. This should also be accompanied by a remark-internal ‘Update when UniProt AC available’

The update will take ~8 weeks to work through the UniProt release system.

Example:

Create an internal protein  
Add identifier from UniProt \(e.g.  p07948-n\) as the Short Label \(n should be a number not yet used by UniProt - if in doubt use 99\)  
Copy the correct isoform sequence from UniProt into the "Sequence box"  
Add a Uniprot xref  to the isoform qualifier = identity  and IntAct xref to the parent UniProt entry - in the example below to P07948:

| **Database** | **Identifier** | **Qualifier** |
| :--- | :--- | :--- |
| UniProtKB | P07948-n | identity |
| IntAct | EBI-79452 | isoform-parent |

Sequence features, such as mutations, within a specific isoform should be mapped to the sequence of that isoform where it differs from the sequence as given in the canonical entry. If an isoform is shown to bind to an interactor and another isoform of the same interactor is shown not to bind, a negative experiment/interaction should be entered \(see 4.6.9\).

### 6.1.3 Problems with mapping accession numbers/Special or Unusual situations

Ubiquitin: Ubiquitin is encoded by 4 different genes \(in mammals\) and cleaved from a larger precursor protein. If the Ubiquitin species is known, but not the exact origin, it can be entered as a pre-existing IntAct protein “ubiq\_human” or ubiq\_mouse etc…

IPI \(deprecated\) database isoform identifiers: do NOT enter isoform information **unless** peptide evidence is available to show that a specific isoform is present.

### 6.1.4 UniProtKB entries that contain multiple protein molecules

All molecules in UniProtKB/Swiss-Prot have the Feature ‘chain’ with a non-redundant PRO ID assigned to it. These indicate poteins that have been cleaved into one or more smaller proteins or bioactive peptides e.g. POMC – \(UniProt Human entry: P01189\). This precursor polyprotein is enzymatically split into 11 smaller proteins/peptides including ACTH and MSH.

Each of these peptides has a distinct identifier in UniProtKB, known as a “Feature identifier” and this ID can be found in the parent UniProt entry under “Sequence annotation \(Features\)” e.g. for ACTH the identifier is PRO\_0000024969.

![](../../.gitbook/assets/0%20%285%29.png)

This “Feature ID” gives the exact sequence present in the molecule and is linked to the parent sequence. Naturally occurring peptides, processed peptides and polyproteins all have these “Feature ids” and these can be used to identify these molecules.

When entering a post-translationally processed chain, such as a viral protein or bioactive peptide cleaved from a longer precursor molecule, in the IntAct Database editor, enter a “FeatureIdentifier” into the import tool – NOT the parent UniProt identifier.

Example: 1. NFKB1

NFKB1 \(KBF1\) is in UniProtKB as accession number P19838  

| NF-kB1/p105 | P19838 | full length |
| :--- | :--- | :--- |
| NF-kB1/p50 | P19838 | from N term to end of glycine rich region range 1-433 has identifier P19838-PRO\_0000030311 |

The processed form \(the p50 subunit\) of NFKB1 does not have a separate entry to the full-length protein in UniProtKB, but is differentiated by the PRO identifier.

Example: 2. Polyproteins

Polyproteins are proteins that are synthesized as a single polypeptide and then cleaved into several distinct proteins.

e.g. viral HIV-1 **Gag-Pol polyprotein Q73368**

Integrase has a Feature ID of PRO\_0000250983 – typing this into the import tool of the editor will create the correct protein participant.

### 6.1.5 Synthetic Peptides

A chemically synthesised peptide can be added as an interactor in a variety of ways:

If the peptide maps to an existing UniProt ID, this can be entered and the exact amino acid sequence numbering entered as a Feature of the type “Sufficient to Bind”. The “Biosource” will be entered as “Chemical synthesis” under “expressed in”.

If the sequence is very dissimilar to anything found in UniProt, it can be added as a “New Interactor” of the Type “Peptide”, and “Organism” = Chemical Synthesis. The sequence of the peptide should be entered in this instance.

Alternatively, and generally only when a modified peptide has been created as a chemical agent, a new ChEBI entry can be requested, and this ChEBI identifier entered as an interactor \[see section 9.2\].

Many synthetic peptides will have been synthesised based on an existing UniProtKB protein/peptide entry but with a few additional linker amino acids. These linkers can be ignored as they do not participate in the interaction, so the UniProt ID with the range added as a feature can be used as an ID \(see above\). Linker amino acids can be added as a ‘mutant’ or ‘tag’ if important.

If there is an ambiguity in assigning a species to a peptide i.e. the identical peptide is conserved across several species, the species can be entered as the same as that of the other interactor\(s\) in the specific interaction. Map the peptide to the appropriate UniProtKB entry and enter the range as a “Sufficient to Bind” Feature.

### 6.1.6 Proteins of unknown species

Interactions cannot be entered unless we can be certain of the origin of the proteins used and can find a database entry. If the paper does not state the species of the protein, it cannot be traced by the curator, and there is no response from the authors of the paper then we will have to disregard these data. In this instance a Data-Processing comment should be added at either Publication and/or Experiment level stating that the proteins cannot be identified and why.

### 6.1.7 Protein update

This is a 4-weekly re-mapping of IntAct proteins to updated UniProt entries.

UniProtKB may update the proteins, merge, or de-merge entries, and assign them new accession numbers or some of the proteins may be retired because of changes to the underlying gene models. These are taken care of during the scheduled UniProtKB update. The retired proteins are identified, and where possible remapped. Where this is not possible, the protein is retained and an attempt will be made with each update to complete the remapping – the interaction will not be lost. When a TrEMBL entry is merged with, or itself becomes a Swiss-Prot entry, the data is mapped to the canonical sequence, even if the transcript the data was originally mapped to becomes an isoform. This could lead to the loss of interesting information, so curators are encouraged to request isoforms only present in TrEMBL to be merged into Swiss-Prot entries prior to commencing curation. Where the update results in two participants being identical these are merged in an interaction and the interaction may consequently have fewer participants. This will be recorded on the interaction, or should be done manually by the curator if observed when first creating the entry. The ranges – where assigned – are also checked for their validity and a range update is carried out with respect to the newer accession.

The schematic of the update procedure can be found at [https://drive.google.com/file/d/0B3S9Q1JQ2DygZTFkMGZiMDgtMDk0Ni00OTAzLWEzZjktMjEwNDA2OGQ4NzMx/view](https://drive.google.com/file/d/0B3S9Q1JQ2DygZTFkMGZiMDgtMDk0Ni00OTAzLWEzZjktMjEwNDA2OGQ4NzMx/view).

## 6.2 Small Molecules

IntAct uses the Chemical Entities of Biological Interest \(ChEBI\) database definition of a small molecule or molecular entity. ChEBI is a freely available dictionary of molecular entities focused on ‘small’ chemical compounds. The term ‘molecular entity’ refers to any constitutionally or isotopically distinct atom, molecule, ion, ion pair, radical, radical ion, complex, conformer, etc., identifiable as a separately distinguishable entity. The molecular entities in question are either products of nature or synthetic products used to intervene in the processes of living organisms. All small molecules should have a ChEBI xref.

Interactions involving small molecules will be annotated wherever possible, but it is not our usual policy to include papers which describe only interactions involving these molecules, unless they are received as a direct submission. Data will only be added when sufficient detail is available to be sure that the small molecule is directly binding to the molecule in question, for example molecules present in a buffer will not be added even if the author states they play a role in the interaction, unless experimental evidence of this is given in the paper.

1. Crystallisation papers – For a small molecule ligand to be seen as binding within a crystal it must be within 3.5Å of the protein, and should not be included in crystals produced at lesser resolution. Modelled ligands should not be included. Care should be taken to separate out binding molecules from crystallisation solution contaminants – normally this should reflect the detail in the paper rather than the wwPDB entry.
2. Cofactors – these will only be added if appropriate data is available to be confident that the molecule is binding to a protein i.e. titration curves, competition analysis etc.

Protein/peptide derivatives do not count as small molecules in the ChEBI definition and we should attempt to map these to parent proteins as tagged or fusion molecules when possible. Example: Experiment EBI-371686 and Interaction EBI-371689.

In this experiment, purified TBP was bound to a TATA box sequence, and then purified Mot1 was added. The interaction between Mot1 and TBP was detected by the change in DNA anisotropy when Mot1 was added to TBP pre-bound to DNA.

## 6.3 Nucleic Acids

IntAct policy is only to annotate interactions involving DNA when either the sequence is given in the publication or an exact match can be found in the ENA database.

For interactions involving RNAs, non coding RNAs entries are created in IntAct using RNA central ID.

mRNAs entries are created using Ensembl transcript ID plus RefSeq.

## 6.4 Macromolecular complexes

Please use Complex Portal identifiers \([www.ebi.ac.uk/complexportal](http://www.ebi.ac.uk/complexportal)\) to represent complexes in IntAct. If a complex is missing, you can request it via [www.ebi.ac.uk/support/complexportal](https://www.ebi.ac.uk/support/complexportal).

## 6.5 Genes

Genes should be given an Ensembl/EnsemblGenomes XRef.

## 6.6 Experimental and Biological roles

The Protein roles are split into biological role and experimental role in PSI2.5. **See** [www.ebi.ac.uk/ols/ontologies/mi](http://www.ebi.ac.uk/ols/ontologies/mi).

 Note that this refers to the role that entity plays within the specific experiment i.e. a protein will only be given the biological role ‘enzyme’ in an enzymatic reaction, not in two hybrid experiment.

### 6.6.1 Experimental role

The role played by the participant in the context of the experiment.

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Experimental Role</b>
      </th>
      <th style="text-align:left"><b>Comment</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Bait</td>
      <td style="text-align:left">
        <p>Bait must always have one or many prey(s)<b>.</b> If there is an interaction
          with prey(s) there must be a bait.</p>
        <p>The bait is in general the protein which is used to isolate other proteins
          which bind to it. The bait may be immobilised during an experiment, be
          tagged or have an antibody raised against the protein itself (anti-bait)
          to aid purification.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Prey</td>
      <td style="text-align:left">Protein(s) isolated by binding to a bait molecule.</td>
    </tr>
    <tr>
      <td style="text-align:left">Unspecified</td>
      <td style="text-align:left">The experiment is such that proteins should have a bait/prey relationship
        but the author has not specified which is which.</td>
    </tr>
    <tr>
      <td style="text-align:left">Self</td>
      <td style="text-align:left">
        <p>Only proteins that have been proven to interact intra-molecularly should
          be given the role &apos;self&apos; (Example: autophosphorylation or disulphide
          bond).</p>
        <p>Where the same protein has been modified in different ways, (Example:
          tagged with different tags) and these molecules are shown to interact,
          these are considered as non-identical subunits. They should be entered
          as separate proteins with the role neutral component or bait/prey as appropriate
          to the experiment and the tags used described as features of the protein.
          See 11.11 for further details</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Putative Self</td>
      <td style="text-align:left">
        <p>Where the interaction is shown to involve molecules of identical sequence
          and modifications but a possibility of inter-molecular interaction exist
          are given the role &#x2018;putative-self&#x2019;.</p>
        <p>The term &#x201C;putative self&#x201D; is used more frequently than &#x201C;self&#x201D;,
          as it is often not known if a molecule is interacting inter- or intra-molecularly
          or both.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Neutral component</td>
      <td style="text-align:left">
        <p>Used when there is no directionality (e.g. bait/prey) in the experiment
          &#x2013; all molecules play the same role, for example when a protein complex
          is isolated by molecular sieving. Role neutral component is often observed
          with stoichiometry determination or oligomerisation studies.</p>
        <p>Unmodified identical proteins may be shown to self-associate using techniques
          such as density gradient sedimentation, non-denaturing gel electrophoresis,
          mass spec, crystallography, and gel filtration (size exclusion chromatography).
          These will be entered as neutral component components. The number of molecules
          interacting will be indicated by stoichiometry (section 5.11)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Acceptor fluorophore/Donor fluorophore</td>
      <td style="text-align:left">Used in conjunction with fluorescence transfer experiments such as FRET.
        Some of the common donor acceptor pairs are CFP/YFP, BFP/GFP, GFP/Rhodamine
        and FITC/Cy3. This method detects interaction by demonstrating proximity
        of 1-10 nm. In the case of BRET and HTRF assays there is a fluorescence
        acceptor and the protein coupled to the molecule giving the fluorescence
        is assigned the role fluorescence donor.</td>
    </tr>
    <tr>
      <td style="text-align:left">Fluorescence acceptor/donor pair</td>
      <td style="text-align:left">Used in conjunction with fluorescence transfer experiments when a single
        molecule is tagged with both tags to demonstrate an intra-molecular interaction</td>
    </tr>
  </tbody>
</table>

### 6.6.2 Biological role

This is used to capture the physiological role of an interactor in a cell or in vivo environment, which is reproduced in the current experiment.

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Biological Role</b>
      </th>
      <th style="text-align:left"><b>Comments</b>
      </th>
      <th style="text-align:left"><b>Example</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Self</td>
      <td style="text-align:left">
        <p>Only proteins that have been proven to interact intra-molecularly should
          be given the role &apos;self&apos; (Example: autophosphorylation or disulphide
          bond).</p>
        <p>Where the same protein has been modified in different ways, (Example:
          tagged with different tags) and these molecules are shown to interact,
          these are considered as non-identical subunits. They should be entered
          as separate proteins with the role neutral component or bait/prey as appropriate
          to the experiment and the tags used described as features of the protein.
          See 11.11 for further details</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Putative Self</td>
      <td style="text-align:left">
        <p>Where the interaction is shown to involve molecules of identical sequence
          and modifications but a possibility of inter-molecular interaction exist
          are given the role &#x2018;putative-self&#x2019;.</p>
        <p>The term &#x201C;putative self&#x201D; is used more frequently than &#x201C;self&#x201D;,
          as it is often not known if a molecule is interacting inter- or intra-molecularly
          or both.</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Electron acceptor/donor</td>
      <td style="text-align:left">Use where the interaction involves a transfer of electrons.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Phospho-donor/acceptor</td>
      <td style="text-align:left">Use when the interaction involves a transfer of phosphate groups. This
        term is NOT used for Protein Kinase Assays, but can be used for Phosphotransferase
        assays /bacterial 2 component transfer systems.</td>
      <td style="text-align:left">EBI-6429292, EBI-6429316</td>
    </tr>
    <tr>
      <td style="text-align:left">Stimulator</td>
      <td style="text-align:left">Use when a molecule increases an interaction by interacting with one or
        more of the participants and it is not essential for the interaction.</td>
      <td
      style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inhibitor</td>
      <td style="text-align:left">Use when the interaction detection technique indicated interaction between
        the inhibitor and inhibited molecule. This could be at a prey/enzyme target
        binding site or a site that modifies the binding site.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Electron acceptor/donor</td>
      <td style="text-align:left">Use where the interaction involves an exchange of electrons.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Enzyme/Enzyme Target</td>
      <td style="text-align:left">
        <p>An <b>enzyme</b> must always have an <b>enzyme target</b> (and vice&#x2013;versa).</p>
        <p>The enzyme (example: kinase) modifies at least one of the interactor/s
          and the target is the modified interactor.</p>
        <p>In the case of autocatalysis e.g. Autophosphorylation, the protein may
          have both roles indicated by using self/putative self.</p>
        <p>Trans-catalysis:</p>
        <p>2 molecules</p>
        <p>Experimental role &#x2013; neutral</p>
        <p>Biological role &#x2013; enzyme/enzyme target
          <br />
        </p>
        <p>Autocatalysis (when proven):</p>
        <p>1 molecule (unless differentiated by tags, mutants etc.)</p>
        <p>Experimental role &#x2013; self</p>
        <p>Biological role &#x2013; self</p>
        <p>Autocatalysis (uncertain):</p>
        <p>1 molecule (unless differentiated by tags, mutants etc.)</p>
        <p>Experimental role &#x2013; putative self</p>
        <p>Biological role &#x2013; putative self</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Cofactor</td>
      <td style="text-align:left">This will normally be used in conjunction with enzyme/enzyme target for
        enzymes where the presence of cofactor has been shown to be required for
        the interaction.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Competitor</td>
      <td style="text-align:left">This interactor binds to the bait molecule in competition with other prey
        molecules.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Unspecified</td>
      <td style="text-align:left">Used when the biological role of the interactor is difficult to ascertain.</td>
      <td
      style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Ancillary</td>
      <td style="text-align:left">Additional interactor within an interaction whose role is not clearly
        defined &#x2013; used in conjunction with molecules which do have clearly
        defined roles</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

## 6.7 Expressed-In \(NA-MIMIX\)

**'**Expressed-in**'** refers to the source/origin of the protein when this is not the same as the Host organism in which the experiment was carried out. If possible, this field should always be filled-in for ‘_in vitro_’ experiments. Leaving the field on --select-- indicates a protein expressed by the system in which the interaction is being measured, i.e by the host organism in which case it need not be entered twice

.

The protein may come from any of the following sources:

**Example:** Protein A is a human protein expressed in baculovirus-infected Sf9 cells, then purified and mixed with Protein B which is an endogenous protein from a nuclear extract from HeLa cells

Experiment Host organism: _in vitro_

Interaction: Protein A ‘Expressed In’ Sf9 cells

\(enter spofr-sf\_9 -_Spodopterafrugiperda_ insect cells\)

Protein B: ‘human-hela’

### 6.7.1 Heterologous protein expression

Heterologous expression means that a protein \(or more usually, the corresponding cDNA\) is experimentally added into a cell that does not normally express that protein. Proteins may be given the additional annotation ‘Experimental Preparation’ and a choice from the drop-down menu e.g. ‘electroporation’.

### 6.7.2 In vitro transcribed and translated proteins

_In vitro_ transcribed and translated are entered in the ‘Expressed in’ box as “in vitro”, for example the production of \[35S\]-Methionine radiolabeled proteins.

### 6.7.3 Synthetic peptides

Please see section 5.8.2.8. The ‘Expressed in’ is ‘chemical synthesis’.

## 

## 6.8 Stoichiometry

Only integer values are accepted. These values are entered as stoichiometry on each individual participant. Where only two purified components have been shown to interact and the experimentally determined stoichiometry is reported as a fraction, approximate the stoichiometry of the interactors to the nearest integer. In the case of assemblies a real fractional stoichiometry may be observed between the components of the interaction, here the stoichiometry must be entered rounded up/down to nearest whole integer. The editor now has the capability of entering a stoichiometry range but in the case of experimental data, the min and max value should generally be identical.

Where a higher assembly is clearly indicated but the number of molecules involved in the complex is not clear, the interactor must be entered twice with stoichiometry of ‘0’ for each and a comment made on the interaction to indicate a higher order complex formation. Examples would be a complex eluting in void volume for a molecular sieving chromatography or an observed higher order gel pattern. Multiple interactions must be entered where the stoichiometry of individual interactors is different e.g. a protein has been shown to exist as both a homodimer and homotetramer.

If two regions \(each purified **separately**\) of the same protein are interacting but it is unclear if this is an intra- or inter- molecular interaction, the molecule must be entered twice with stoichiometry ‘0’. The Experimental Roles of the interactors are ‘putative self’ and the Interaction Type _‘_self interaction’.

Identical molecules but with differing tags should be treated as distinct participants and the stoichiometry of each separately entered.

Briefly: for oligomers/dimers etc.

If the number of molecules is KNOWN: enter molecule ONCE; stoichiometry = number of molecules.

For homo-oligomers, if the number of molecules is NOT KNOWN: enter molecule TWICE, stoichiometry = “0”.

If a dimer and a trimer are both formed, enter two separate interactions.

The fields “Min Stoich” and “Max Stoich” should have the same values entered – a range is only entered for Complex curation.

Additionally, the GO cross-reference ‘protein homooligomerization’ GO:0051260 can be added at the Interaction level.

## 6.9 Participant name alias

The author-identifiers, when different from the gene name or ID, may be added onto a participant as an ‘alias’ under “author given name”. This is important in the curation of large scale datasets to keep a record of the mapping of the original data. This is a defined field and can be added using the drop-down menu in the tabbed field ‘Alias’

## 6.10 Annotations \(unique to Participant-level\)

The annotations for individual participant properties should be added on the participant.

### Experimental Preparation

This is the method by which a molecule is delivered or engineered into a cell. This annotation can include the terms electroporation, microinjection or nucleic acid delivery. This is a defined field and can be added using the drop-down menu in the tabbed field ‘Experimental preparation\(s\)’. Additional information may be added as a Comment.

It is mandatory to annotate \(according to the case\) information that cannot be inferred from the experiment itself: 

‘expression level’ for protein expressed in living cells, fixed cells or in cell lysate:

 -over expressed

 -under-expressed

 -physiological level

And sample process for purified or semi purified proteins

 - ‘purified’

 - ‘partially purified'

**Identification Method:** can be added for individual participants when the participant is detected by a different method from that given at Experiment level. This will override Participant Detection at Experiment level. This is a defined field and can be added using the drop-down menu in the tabbed field ‘Identification method\(s\)’.

Any parameter associated with a wild-type protein is generally added at the interactions level. This is a defined field and can be added using the drop-down menu in the tabbed field ‘Parameter’

Definition of terms on this menu can be found in OLS \(Molecular Interactions\): [www.ebi.ac.uk/ols/ontologies/mi](http://www.ebi.ac.uk/ols/ontologies/mi).

