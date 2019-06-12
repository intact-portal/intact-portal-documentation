# 4. Experiment level

The experiment records the experimental method used to demonstrate the interaction\(s\). One experiment may have many interactions linked to it; these interactions must all share the **same** experimental protocol. Within one Publication, multiple identical interactions can be found with every interaction being in a separate Experiment, due to differing experimental protocols being used for each individual interaction.

**Note:** The converse is not allowed i.e. one interaction may **not** belong to multiple experiments.

Experiments that demonstrate that an interaction does **not** occur can be entered in IntAct under special conditions. See: Annotation Topics 'Negative', section 4.6.9.

Example of an Experiment – with two interactions.

![](../../.gitbook/assets/0%20%282%29.png)

## 4.1. Experiment AC

A unique AC number is assigned to the experiment when you click the ‘save’ button. Searches on this number will bring up the entry.

## 4.2 Experiment Short Label

This is a mandatory field. It is normally automatically generated in the form “zhang-2012c-4”or similar. However errors can arise, so in order to correct these it is necessary to know that:

An experiment Short Label has the following format:

\[first author last name\]-\[year of publication\]\[optional char\]-\[integer\]

Overall character limit is 256.

All characters that are not in \[a-z\] are replaced by \_ \(underscore\).  
The Short Label is lowercase.  
When the name of an author has been used more than once \(different PubMed ID\) in the **same year**, enter year a, b, c etc. after the year of publication as illustrated below, based on the chronological order in which the data was entered in IntAct.

e.g. stargell-2003-1  
    stargell-2003a-1  
The experiment number or final integer will be added based on the  
chronological order of entering the data in IntAct.

## 4.3 Host organism

This is a mandatory field.

The Host Organism indicates where the experiment has been performed. The Host Organism \(plus tissue or cell-line, if relevant\) is chosen from a drop down list of organisms. This menu uses the UniProt organism identifier code which provides a 5 letter code by which each organism may be differentiated. For example, the 5 letter code for “dog” = “CANFA” \(the first 3 letters from **Can**is and first 2 from **fa**miliaris\).

Additional information on the species level, for example details sub-species level, should be added in the annotation topic ‘exp-modification’. For cell lines that have been modified, the host organism will be the unmodified cell line and the modification will be entered under annotation topic ‘exp-modification’. Similarly when entering experiments from multiple cell lines which are very closely related \(for example T-REX cell are a sub-line of HEK293 cells\), you can enter one cell line, rather than several. Tissue and cell type should be used as host organism where applicable.

### 4.3.1 In vitro experiments

The interactions occur outside of the intact cellular environment. Experiments carried out literally “in glass”, or commonly called "experiments in a test tube". Examples of when ‘Host Organism’ is _in vitro_:

#### 4.3.1.1 Extracellular experiments

If one of the interacting proteins is extracellular or has an extracellular domain that participates in the interaction e.g. receptor-protein ligand interactions where the ligand is extracellular, the interactions are classed as **“**_**in vitro**_**’’**. For a definition of extracellular see [GO:0005576](https://www.ebi.ac.uk/QuickGO/term/GO:0005576).

Interactions in which the interacting proteins are membrane-bound and the interaction is through their extracellular domains \(e.g. by FACS analysis\) are classed as **“**_**in vitro**_**.”**

Example of the interaction of a receptor with a protein ligand by cross-linking and co-immunoprecipitation: [EBI-80473](http://www.ebi.ac.uk/intact/pages/details/details.xhtml?experimentAc=EBI-80473)

Example of interactions using cross-linking and 2D gels [EBI-368460](http://www.ebi.ac.uk/intact/search/do/search?searchString=EBI-368460&searchClass=Experiment&filter=ac)

\[**Note:** The following receptor based interactions are curated as **“**_**in vivo”**_

1. both the interacting proteins are membrane bound and it is not known if the interaction is in the extracellular, intracellular or transmembrane domain and cell lysate is used for determining interaction.

2. the study is carried out in a cell lysate and it cannot be determined if the interaction is between cells or within the same cell.\]

#### 4.3.1.2 Experiments between intracellular proteins demonstrated ex vivo

The interaction occurs out of the cellular environment e.g. on a column, in an instrumental cell, on a biosensor, a crystal. The components of the interaction may be purified or semi-purified and each component could come from any of the sources below.

i\) Purified proteins: The proteins may be expressed in a heterologous system example: _E. coli_, yeast, insect, mammalian or/and plant cells and purified from these or from its natural source.

ii\) Proteins are from more than one cell lysate

iii\) Secreted protein

iv\) _In vitro_ transcribed and translated protein

v\) Synthetic peptide

vi\) Purified peptide

vii\) Proteins embedded in the phospholipid bilayer, liposome or micelles

Details of heterologous protein expression for each protein must be entered in the ‘Expressed In’ on the interaction page.

### 4.3.2 In vivo experiments

The proteins interact within an intact cellular environment. All of the interacting proteins must be expressed in a cell or cell membrane; an exception would be micro-injected proteins. The proteins may be modified \(tags, promoters, fragments, crosslinks\). The cell may be subsequently lysed to enable access to an immuno-precipitating antibody or other detection agent.

The names of cell lines and tissue types used when the interaction is demonstrated to occur _in vivo_ should be added in the experiment under “host organism”. To create a ‘Host Organism’ or ‘BioSource’ please refer to Section 8.1. If the protein has been overexpressed or expressed at endogenous levels this information should be stored in annotation topic ‘expression-level’. When the proteins are expressed in the same organism in which the interaction is occurring, the organism should **not** be redundantly added as ‘expressed-in’

Example:

1. Human proteins A and B are expressed in Cos-7 cells and shown to interact by coimmunoprecipitation.

Experiment: Host Organism: Cos-7 cells \(chlae-cos\_7\)

**Note:** In this experiment the host organism is C. aethiops \(African green monkey\) as the proteins were expressed in Cos cells and the complex was formed in Cos cells.

2. One cell expressing two or more transmembrane proteins and the intracellular domains or transmembrane regions are demonstrated to interact, for example by in vivo cross-linking using a cross-linker that crosses the cell membrane.

3. Detection of protein-protein interactions in live cells using techniques such as FRET \(fluorescence resonance energy transfer\) or BRET \(bioluminescence resonance energy transfer\).

4. Coimmunoprecipitation of proteins from a single extract or lysate.

5. Fractionated proteins - proteins are in a fractionated cell extract from cell lines, embryos or tissues. This refers to complexes pre-formed in cells and purified through subsequent steps. Example: cell extract, nuclear extract, vesicle fraction, Golgi membranes, membrane fraction.

6. If the membrane has been purified with the proteins and interactions within the membrane are studied this would then classify as _in vivo_ interaction.

### 4.3.3 Viral/Bacterial Strains

For Viral or Bacterial Strains, we map to the strain level, if this is known.

If you do **not** know the exact strain used, as is frequently the case, take your UniProtKB identifiers from the [Reference Proteome](http://www.uniprot.org/faq/47).

## 4.4 Interaction Detection Method

This is a mandatory field. Add a term by selecting from the drop-down menu.

Use the term from the hierarchy of the controlled vocabulary that describes the interaction detection as closely as possible. Experiments where the interaction detection technique used is a child term of ‘post transcriptional interference’ or ‘genetic interaction’, “Genetic Reporter Assay” or “phenotype-based detection assay” are not entered in the IntAct database.

### 4.4.1 Examples of common interaction detection techniques

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Method</b>
      </th>
      <th style="text-align:left"><b>Experiment no.</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">molecular sieving</td>
      <td style="text-align:left">
        <p>EBI-2911349, EBI-5668263</p>
        <p><a href="http://www.ebi.ac.uk/intact/interaction/EBI-4305071?conversationContext=2">EBI-4305071</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Fps</td>
      <td style="text-align:left">EBI-2941846, <a href="http://www.ebi.ac.uk/intact/interaction/EBI-2877525?conversationContext=2">EBI-2877525</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">anti tag coimmunoprecipitation (in vitro)</td>
      <td style="text-align:left"><a href="http://www.ebi.ac.uk/intact/interaction/EBI-2911101?conversationContext=2">EBI-2911101</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">anti bait coimmunoprecipitation (in vivo)</td>
      <td style="text-align:left">EBI-5378672</td>
    </tr>
    <tr>
      <td style="text-align:left">Cosedimentation (density gradient)</td>
      <td style="text-align:left"><a href="http://www.ebi.ac.uk/intact/interaction/EBI-6127934?conversationContext=2">EBI-6127934</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Cosedimentation (solution)</td>
      <td style="text-align:left"><a href="http://www.ebi.ac.uk/intact/interaction/EBI-3989600?conversationContext=2">EBI-3989600</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Far western</td>
      <td style="text-align:left"><a href="http://www.ebi.ac.uk/intact/interaction/EBI-2943702?conversationContext=2">EBI-2943702</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">fluorescence spectr</td>
      <td style="text-align:left"><a href="http://www.ebi.ac.uk/intact/interaction/EBI-1774733?conversationContext=2">EBI-1774733</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Facs</td>
      <td style="text-align:left"><a href="http://www.ebi.ac.uk/intact/interaction/EBI-3870457?conversationContext=2">EBI-3870457</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">pull down</td>
      <td style="text-align:left">
        <p><a href="http://www.ebi.ac.uk/intact/interaction/EBI-2911426?conversationContext=2">EBI-2911426</a>,
          <a
          href="http://www.ebi.ac.uk/intact/interaction/EBI-6138583?conversationContext=2">EBI-6138583</a>,</p>
        <p><a href="http://www.ebi.ac.uk/intact/interaction/EBI-5912162?conversationContext=2">EBI-5912162</a>,
          <a
          href="http://www.ebi.ac.uk/intact/interaction/EBI-4481555?conversationContext=2">EBI-4481555</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">protein crosslink</td>
      <td style="text-align:left">EBI-3960025</td>
    </tr>
    <tr>
      <td style="text-align:left">Itc</td>
      <td style="text-align:left"><a href="http://www.ebi.ac.uk/intact/interaction/EBI-2655240?conversationContext=2">EBI-2655240</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Spa</td>
      <td style="text-align:left">EBI-23597562</td>
    </tr>
    <tr>
      <td style="text-align:left">x-ray diffraction</td>
      <td style="text-align:left"><a href="http://www.ebi.ac.uk/intact/interaction/EBI-2464773?conversationContext=2">EBI-2464773</a>,
        <a
        href="http://www.ebi.ac.uk/intact/interaction/EBI-2213576?conversationContext=2">EBI-2213576</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Fret</td>
      <td style="text-align:left"><a href="http://www.ebi.ac.uk/intact/interaction/EBI-4373847?conversationContext=2">EBI-4373847</a>,
        <a
        href="http://www.ebi.ac.uk/intact/interaction/EBI-6127663?conversationContext=2">EBI-6127663</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Nmr</td>
      <td style="text-align:left">EBI-6264210, <a href="http://www.ebi.ac.uk/intact/interaction/EBI-3507479?conversationContext=2">EBI-3507479</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">dhfr reconstruction</td>
      <td style="text-align:left"><a href="http://www.ebi.ac.uk/intact/search/do/hvWelcome?searchString=EBI-448165">EBI-448165</a>,
        <a
        href="http://www.ebi.ac.uk/intact/search/do/hvWelcome?searchString=EBI-1296">EBI-1296</a>, EBI-6313895</td>
    </tr>
    <tr>
      <td style="text-align:left">molecular sieving</td>
      <td style="text-align:left">EBI-4305063, EBI-4289462</td>
    </tr>
    <tr>
      <td style="text-align:left">PLA/pELISA-proximity ligation assay</td>
      <td style="text-align:left">EBI-4312047, EBI-6143088</td>
    </tr>
    <tr>
      <td style="text-align:left">BiFC</td>
      <td style="text-align:left">EBI-6097675</td>
    </tr>
    <tr>
      <td style="text-align:left">FRET</td>
      <td style="text-align:left">EBI-5544932, EBI-5240070, EBI-6162091</td>
    </tr>
    <tr>
      <td style="text-align:left">Crosslink</td>
      <td style="text-align:left">EBI-3959976, EBI-4533282</td>
    </tr>
    <tr>
      <td style="text-align:left">confocal microscopy</td>
      <td style="text-align:left">EBI-3950472, EBI-3863350</td>
    </tr>
    <tr>
      <td style="text-align:left">spr</td>
      <td style="text-align:left">EBI-4406354 , EBI-5452477</td>
    </tr>
    <tr>
      <td style="text-align:left">two hybrid (library screen)</td>
      <td style="text-align:left">EBI-6309959</td>
    </tr>
    <tr>
      <td style="text-align:left">Two hybrid</td>
      <td style="text-align:left">EBI-6313541</td>
    </tr>
    <tr>
      <td style="text-align:left">Tandem Affinity purification (TAP)</td>
      <td style="text-align:left">EBI-4374417, EBI-2130618</td>
    </tr>
  </tbody>
</table>Further examples of interactions using a particular Interaction Detection Method in IntAct can be found by locating the MI number \(PSI-MI accession number\) for the method in OLS \(Ontology Lookup Service\): [www.ebi.ac.uk/ols/ontologies/m](http://www.ebi.ac.uk/ols/ontologies/mi)[i](http://www.ebi.ac.uk/ols/ontologies/mi)

After you have found the MI number enter it into the “Advanced Fields” search on the IntAct web page, under the Field “Interaction Detection Method”.

If the method as described in the publication does not exist in the drop-down menu search for it in OLS as it may be a synonym.

Additional experimental detail, for example variations from standard protocols, should be added as an &lt;Annotation&gt; “Experimental Modification \(Exp-Modification\)”.

Purification of a protein complex may be a sequential process. If the process can be annotated to a common parent e.g. ‘chromatography technology’, this should be selected. If this cannot be achieved, the curator needs to select a key step in the purification process which separates the complexes out from a protein mix. When a multi-step purification procedure takes place, and a figure is shown for participant ID at each stage, the whole process should be curated in separate steps. Where a "double pulldown" is performed Protein A-His, Protein B-Flag e.g. anti-His column, followed by anti-Flag column, followed by participant determination should be entered twice bait/prey, prey/bait.

Cross-linking will almost always be taken as inferring any subsequent isolation technique, which will not be separately captured. In cross links, if the subsequent isolation technique employee a protein as ‘bait’, participants will be annotated to have experimental roles ‘bait’ and ‘prey\(s\)’

### 4.4.2 Enzyme Assays

There has been debate as to whether an immunoprecipitated enzyme preparation is 'clean' enough to be used in an in vitro enzyme assay, or if the data should NOT be added as other enzymes may also be pulled down in the same preparation and may actually be the active factor in any subsequent assay. Enzyme assay data should therefore only be captured under one or more of the following circumstances:

1. The author \(or commercial producer\) describes further purification of an enzyme beyond just an initial IP.  
2. The author shows by stained gel that the preparation is pure.  
3. The enzyme activity is monitored by radioisotope incorporation, an autoradiograph is performed and the author shows the entire gel, and no other bands are present suggesting contamination.

The activity, and resulting process should also be captured using appropriate GO terms cross-referenced at the interaction levels, for example a protein kinase assay should have:

[GO:0004672](http://www.ebi.ac.uk/intact/interaction/EBI-2941958?conversationContext=2) protein kinase activity

[GO:0006468](http://www.ebi.ac.uk/intact/interaction/EBI-3870792?conversationContext=2) protein phosphorylation OR [GO:0046777](http://www.ebi.ac.uk/intact/interaction/EBI-2941958?conversationContext=2) protein autophosphorylation

**Resultant ptms**

The results of an enzyme interaction may be captured by adding the ‘resultant ptm’ as a feature on the Participant that is the “Enzyme Target”, using the following syntax:-

**Shortlabel**: enter the amino acid and residue number affected - if known, e.g “ser-99”. If the residue is not known enter “region” and range “?-?”.

**Feature Type**: Enter correct Protein Mod term {OLS-MOD CV term}, e.g “opser”

**Feature Role**: Add “resulting-ptm” from the menu.

\[**Note**: This replaces the legacy Annotation topic ‘resulting-ptm’ of the type e.g. P12345 ser-99 O-phospho-L-serine\]

When you curate resulting-ptm features, please add a single feature for each amino

acid/position affected. No multiple ranges should be added in these cases. This is because there are separate CV terms for each phosphorylated amino acid, so each one of them needs to be curated as a separate feature.

When enzyme assays are detected by a radio-labelled transferred molecule e.g. protein kinases, phosphotransferase, sulfurtransferases, the radiolabelled entity is not normally added e.g. ATP need not be added to every kinase assay.

In the case of transferases \(e.g. phosphotransferase, sulfurtransferases\) the biological roles should be the appropriate donor/acceptor rather than enzyme/enzyme target whilst we can only select one role.

## 4.4.3 RNA-protein or RNA-RNA interactions

Some Interaction Detection Methods are specific for RNA-protein or RNA-RNA interactions:

* **Clip \(**MI:2191\) and its variations: **Clip-Seq** \(MI:2192\); **iCLIP** \(MI:2193\); Par-Clip \(MI:2188\)

Combination of cross-linking and co-immunoprecipitation aimed to find protein-RNA interactions. The canonical method uses first a cross-linking procedure over a tissue sample or lysate, followed by immunoprecipitation using antibodies specific for the protein of interest. The protein is the bait and the RNAs are the preys. The detection method can be nucleotide sequence or Northern Blotting

* **CRAC** \(MI:2194\)

Similar to Clip, but the protein of interest bears a tag used for pull-down or immunoprecipitation.

* **CLASH \(**MI:2195\)

Used to detect RNA-RNA interactions that occur in the proximity of an RNA binding protein of interest. The RNA is crosslinked to the protein, that is immunoprecipitated. After RNAsi treatment the RNA hybrids protected from degradation by the protein are ligated and chimeras are sequenced, so the detection method is always nucleotide sequence.

The two RNAs are Neutral Components and the protein, when indicated, can be added as a comment in annotation.

* **Chemical RNA modification plus base pairing prediction** \(MI:2224\)

Used to detect RNA-RNA interactions that guide the chemical modification of the target RNA. RNA-RNA pairings are tested by knocking down one of the two interacting RNAs and then experimentally determine if its presence is required for the other to be chemically modified. The interaction type is a physical association and the participant detection method is often primer extension assay \(MI:2203\). RNAs are neutral components and the modified base must be indicated in features with ChEBI ID \(e.g. PMID:9891049\)

* **Luciferase Assay \(MI:2285 miRNA interference luciferase assay\)**

The mRNA regulative region, often located at the 3’ UTR of the mRNA, is

cloned at the end of the luciferase gene, in suitable vectors. When the plasmid is

co-transfected with the microRNA, the luciferase expression is significantly lowered. The

interaction MUST be confirmed by mutating the microRNA seed sequence site in the 3’

UTR of the mRNA to check that that the sequence is essential i.e. the binding is true

 \(e.g PMID 26184978\). The interaction type is a physical association and the participant  
detection method is tag luciferase for the mRNA and predetermined for the  
microRNA. RNAs are neutral components but there is a causality relation so that  
the microRNA is the regulator and the mRNA is the regulation target.

The mutation in the seed sequence is annotated as a feature of the mRNA.

### Examples of common interaction detection techniques for RNA

| Method | Experiment no. |
| :--- | :--- |
| Clip-seq | EBI-20978107 |
| Crac | EBI-10835868 |
| Clash | EBI-10954258 |
| Chemical RNA modification plus base pairing prediction | EBI-11792756 |
| Luciferase Assay | EBI-21006454 |

**4.5 Participant Detection Method**

This is a mandatory field. Add a term by selecting from the drop-down menu.

‘Participant Detection’ describes the method used for detecting the participants of an interaction. It may refer to detection during, or after the interaction has occurred.

If more than one method is used for Participant Detection in an experiment, the major or predominant method, or that identifying the prey, is entered in the drop-down menu at Experiment level. Any additional methods used can be added directly to the Participant under “Identification Method” from the drop-down menu at Participant level. e.g. in Co-localization experiments participants may be detected by a mixture of Tag Fluorescence and immunostaining \(antibody staining\).

### 4.5.1 Use of ‘Predetermined’ as a Participant detection method

Predetermined \(or child terms\) will be used whenever a group has introduced a known protein into a system and then utilised the fact that they know that this protein is already present in the system as a basis for identification. For example, tagged proteins are expressed in E.coli and purified. They are subsequently mixed and the comigration of the complex \(with proteins identified purely by molecular weight following protein staining\) down a column or in a gel is taken as evidence of an interaction. If using a matrix of known proteins in a two hybrid assay, the participant detection method is ’predetermined’ unless the author has specifically stated that the molecules were subsequently re-sequenced or detected by another method.

Proteins from a lysate **cannot** be identified purely on the basis of molecular weight. If a PMID describes interactions based on participant identification by 'molecular weight estimation by staining' and child terms but NO confirmation of the identity of the participant is available in this publication, this will NOT be curated. This includes purified complexes or dimers inferred by molecular weight from whole cell lysates. These should not be captured as there had been no purification step and other proteins may be responsible for the change in molecular weight. Curation will only commence when a complex has at least been partially purified. A reference to a previous paper is NOT acceptable. However, if a publication has participants identified by 'molecular weight estimation by staining' or a child term but a further confirmation of the participant is obtained by an alternative method such as MS or Western this data CAN be curated. If _in vitro_ purified proteins are used and participants identification using 'molecular weight estimation by staining' or child terms this data CAN be curated.

### 4.5.2 Interaction/Participant Detection Methods

Examples of specific cases, pitfalls for the unwary & some common errors or omissions:

**Interaction Detection Method** **Comment**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Far Western Blotting</th>
      <th style="text-align:left">the protein probe is the bait and the protein interacting with it is the
        prey (which is often immobilised)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Crosslinking</td>
      <td style="text-align:left">any subsequent isolation technique(s), will not be separately captured,
        but entered as an &#x201C;Exp-Mod&#x201D;. If the subsequent isolation
        technique employee a protein as &#x2018;bait&#x2019;, participants will
        be annotated to have experimental roles &#x2018;bait&#x2019; and &#x2018;prey(s)&#x2019;</td>
    </tr>
    <tr>
      <td style="text-align:left">Two hybrid screens</td>
      <td style="text-align:left">When a prey cDNA library is used (for screening) the Participant Detection
        method is &#x201C;nucleotide-sequence&#x201D;. (The &#x201C;library used&#x201D;
        should be added to the Experiment page.)</td>
    </tr>
    <tr>
      <td style="text-align:left">Two hybrid</td>
      <td style="text-align:left">Use &#x201C;Predetermined&#x201D; for participant detection for any further
        two hybrid assays after the initial screen when there has been NO re-sequencing
        of constructs.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Protein Complementation Assays (including multiple children e.g. Y-2-H,</p>
        <p>bifc, dhfr, ubiquitin-reconstruction etc&#x2026;&#x2026;)</p>
      </td>
      <td style="text-align:left">
        <p>Tags need not be added if they are present in the Interaction Detection
          Method. However if there is a choice of tag or the tags are non-standard,
          they should be added.</p>
        <p>NB: all these assays normally have only Binary Interactions &#x2013; one
          Bait-One Prey.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">molecular weight estimation by staining</td>
      <td style="text-align:left">Only enter this data if further confirmation of the participants has been
        obtained by an alternative method such as MS or Western, if <em>in vitro</em> purified
        proteins have been used or in the case of radioactively-labeled, <em>in vitro</em> translated
        proteins obtained with reticulocyte lysate system, where the radiolabeled
        protein is not purified, but it is overwhelmingly dominant in the lysate.</td>
    </tr>
    <tr>
      <td style="text-align:left">Co-IP</td>
      <td style="text-align:left">If preys are detected by two different methods (e.g. anti-tag WB and WB)
        on the same blot enter data for Participant Detection at the highest level
        (Western blot). Alternatively the major or predominant method is entered
        in the drop-down menu at Experiment level. Any additional methods used
        can be added directly to the Participant under &#x201C;Identification Method&#x201D;
        from the drop-down menu at Participant level.</td>
    </tr>
    <tr>
      <td style="text-align:left">Fluorography</td>
      <td style="text-align:left">Enter as autoradiography</td>
    </tr>
    <tr>
      <td style="text-align:left">Mass Spec</td>
      <td style="text-align:left">Enter Participant Detection as &#x201C;MS Participant&#x201D; if no type
        of MS is stated or can be found. Tandem MS (or MS/MS) is entered as &#x201C;Sequence
        Tag&#x201D;.</td>
    </tr>
    <tr>
      <td style="text-align:left">Chip</td>
      <td style="text-align:left">Interaction Detection method is &#x201C;CHIP&#x201D; and Participant detection
        is usually &#x201C;primer specific pcr&#x201D;.</td>
    </tr>
    <tr>
      <td style="text-align:left">ChIP-seq</td>
      <td style="text-align:left">Interaction Detection method is &#x201C;chip&#x201D; and Participant detection
        is &#x201C;nucleotide sequencing&#x201D;.</td>
    </tr>
    <tr>
      <td style="text-align:left">re-ChIP (Sequential ChIP, Chromatin Re-IP and ChIP Re-ChIP)</td>
      <td style="text-align:left">Re-ChIP enables sequential chromatin immunoprecipitations to be performed
        using two different antibodies so that you can assay for the simultaneous
        presence of two proteins or distinct histone modifications at the same
        genomic region of interest, the protein pulled down by the second antibody
        used should be taken as bait, the first protein precipitated and the DNA
        sequence should be taken as prey.</td>
    </tr>
    <tr>
      <td style="text-align:left">EMSA</td>
      <td style="text-align:left">
        <p>This should only be annotated if the sequence of the (labelled) probe
          is given and can be added to a created entry. A cross-reference should
          be added for the probe &#x2013; if possible.</p>
        <p>Roles: The labelled probe is the bait, the bound protein is the prey.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Co-IP (generally entered as anti-bait or anti-prey)</td>
      <td style="text-align:left">Western blots: if it is not clear if the author has stripped and re-probed
        the same blot with multiple antibodies, OR repeated the co-immunoprecipitation
        multiple times and checked each with a single antibody, the experiment
        should be represented once as one bait, many prey interaction.</td>
    </tr>
    <tr>
      <td style="text-align:left">PLA</td>
      <td style="text-align:left">Participant&#x2019;s Experimental role should be &#x201C;Neutral component&#x201D;.
        Interaction Type is &#x201C;Physical Association&#x201D; and Participant
        Detection should be &#x201C;Antibody Detection&#x201D;.</td>
    </tr>
  </tbody>
</table>Further details can be found in the TABLE of PSI-MI dependencies –found here:-

[https://docs.google.com/spreadsheet/ccc?key=0AtAwdqt9ekgYdFpIWTFrWEMxZGRXemdmWHNkS1RPRWc&usp=sharing\#gid=0](https://docs.google.com/spreadsheet/ccc?key=0AtAwdqt9ekgYdFpIWTFrWEMxZGRXemdmWHNkS1RPRWc&usp=sharing#gid=0)

\[TAKE CARE not to type anything in this page, as anything added/altered will be retained!\]

## 4.6 Experiment Annotations \(NA-MIMIx except copyright\)

Annotations on the Editor-Experiment page relate to the experimental conditions only. Annotations related to individual proteins should be entered on the participant. The following annotation topics \(in addition to comment, caution and remark-internal, see 1.7\) may be used while curating an experiment:

### 4.6.1. Antibodies

This annotation can list the specific antibodies used in the interaction detection or participant identification. This detail is not routinely added, but rather when an unusual entity is used.

### 4.6.2. confidence-mapping

This annotation topic gives a description of the method/s used by the author for confidence mapping the interactions attached to this experiment.

In large-scale experiments where the authors of the paper have assigned confidence values to the interactions, the experiment must contain an explanation of the author’s definition of the confidence values. This must be written in the experiment annotation topic ‘confidence-mapping’.

In addition, the author confidence values that are suitable for export to UniProtKB must be added in the experiment annotation topic ‘uniprot-dr-export’

Example: In experiment EBI-332598 the annotation is as follows:

| **Experiment AC** | **Topic** | **Description** |
| :--- | :--- | :--- |
| EBI-332598 | confidence-mapping | The authors have assigned the following confidence values to the interactions: Core-1: found at least three times independently and the AD-Y junction is in frame. Core-2: found less than three times independently, retest positive, AD-Y junction is in frame. Non-core: all other interactions. |
| EBI-332598 | uniprot-dr-export | CORE\_1 |

Historically, we have captured the high and low confidence interactions and filtering is possible based on the values available in author-confidence annotation on interaction. From the Heidelberg 2011 IMEx meeting, only the high confidence interactions will be captured, where the confidence is expressed by the authors as high.

### 4.6.5 copyright \(MIMIx applicable\)

Unusually, individual experiments or interactions might have specific copyright statements attached to them. A copyright statement on experiment level applies to all interactions which are part of the experiment. Copyright statements attached to individual interactions override the statements inherited from the experiment.

Example: [EBI-449125](http://www.ebi.ac.uk/intact/search/do/hvWelcome?searchString=EBI-449125) and [EBI-449126](http://www.ebi.ac.uk/intact/search/do/hvWelcome?searchString=EBI-449126) have the annotation copyright “These interactions are the sole property of HYBRIGENICS, and shall not be used for any business or commercial purposes without the prior written license from HYBRIGENICS \([http://www.hybrigenics.com](http://www.hybrigenics.com/)\)”.

### 4.6.6 data-processing

This annotation topic is used to describe the steps in processing of data to obtain the **identifiers** described in the entry, and placed at the experiment level when only applicable for a specific experiment. Information about the original number of interactions described by the authors in the paper and the corresponding number in IntAct, if different from the one published in the paper, should also be stored here.

**Example:**

A unique UniProtKB entry could not be associated with \(author identifier/name\) since \(organism/subtype/exact gene product\) of interactor cannot be ascertained.

Proteomics Papers: All too frequently with Mass Spec protein identifications, the wrong species is given in the results. E.g. the Experiment uses mouse-ES cells, and manages to identify a “dog” protein. This is likely to be a homologous protein, and a Data-Processing comment should be added of the type: “gi\|51701919\|sp\|P63049\| Ubiquitin is a dog protein - this has been remapped to mouse.”

When the method by which a protein has been identified is not immediately apparent from the original paper, this should be detailed. Format should be

Source of Protein X supplied by author

Source of Protein X taken from PMID: 1234567

Replies from authors confirming or stating the origin/source and/or identity of proteins should be entered here.

If the protein identification is doubtful, do not add the affected proteins to any interactions, and add a Data-Processing comment stating that the proteins have not been added, giving a reason

Some examples of other types of Data-Processing Comments:

<table>
  <thead>
    <tr>
      <th style="text-align:left">EBI-6176354</th>
      <th style="text-align:left">The number of interactions found in the paper following the author&apos;s
        cut-off values is different from the one they give in the text. The authors
        were contacted to clarify this, but no answer was received.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">EBI-6550704</td>
      <td style="text-align:left">The authors state that the Gfi1-Flag contruct used in Fig 5H contains
        the human GFI1 sequence.</td>
    </tr>
    <tr>
      <td style="text-align:left">EBI-6509682</td>
      <td style="text-align:left">
        <p>Origins and details for the Flag-MKK3 and mutant constructs have been
          taken from the Addgene repository. The authors have previously confirmed
          that the FLAG-MEKKS are Human in origin.</p>
        <p>As the authors did not respond to subsequent requests for information,
          the origins of JIP1-4 (gifts from Dr. Roger Davis) have been taken from
          these sources (all quoting RJ Davis as co-author).</p>
        <p>JIP1 (PMID:11562351) = Murine</p>
        <p>JIP2 (PMID:10490659) = Human</p>
        <p>JIP3 (PMID:10629060) = Murine</p>
        <p>JIP4 (PMID: 15767678) = Murine</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">EBI-6548358</td>
      <td style="text-align:left">Tlr11 does not exist in humans. As the authors cloned both Tlr5 and Tlr11
        it has been assumed both are murine.</td>
    </tr>
    <tr>
      <td style="text-align:left">EBI-6511141</td>
      <td style="text-align:left">Origin of ATXNL2 constructs according to PMID 11784712, of ATXN2 constructs
        according to 15663938.</td>
    </tr>
    <tr>
      <td style="text-align:left">EBI-6504820</td>
      <td style="text-align:left">The authors have confirmed that myc/gst tagged 14-3-3 proteins are murine
        in origin, as is PKA (obtained from New England Biolabs).</td>
    </tr>
    <tr>
      <td style="text-align:left">EBI-6513729</td>
      <td style="text-align:left">The species of the &quot;AT&quot; RABL1 construct and amino acid numbering,
        as well as origin of GFP-VPS35 (Fig 7E) is not known. The authors have
        not responded to requests for clarification, so no interactions with these
        constructs have been included.</td>
    </tr>
    <tr>
      <td style="text-align:left">EBI-6512291</td>
      <td style="text-align:left">
        <p>Interactions involving the use of &quot;PKC activity assay from Enzo Life
          Sciences&quot; (Kinase Assay) cannot be entered as the reaction substrate
          is only described as a &quot;peptide&quot; and Enzo does not wish to further
          identify it.</p>
        <p>Interactions involving HSP90 have not been included due to lack of antibody
          specificity.</p>
        <p>The authors have confirmed that the IRS1 Kinase assay substrate is Rattine
          in origin (Millipore 13-124).</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">EBI-6554661</td>
      <td style="text-align:left">Source of Flag tagged Sirt6 and c-myc taken from previous work of the
        author (PMID: 23142079 and 20592034 respectively)</td>
    </tr>
    <tr>
      <td style="text-align:left">EBI-6270859</td>
      <td style="text-align:left">The authors confirm that both TLR3-Flag and TRIL-V5 are of human origin.</td>
    </tr>
    <tr>
      <td style="text-align:left">EBI-2657512</td>
      <td style="text-align:left">
        <p>hnRNP G-T (ref XP_914797) the NCBI states &quot;report removed&quot;,
          remapped to Q9DAE2</p>
        <p>gi|51701919|sp|P63049| Ubiquitin is a dog protein- this has been remapped
          to mouse.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">EBI-2696332</td>
      <td style="text-align:left">gi:480806 - &quot;report removed&quot;, so remapped to P53534. Similarly,
        reports removed or unavailable for: gi:76496512 remapped to P09606, gi:34869154
        remapped to P25286, gi:34879653 remapped to P26284, gi:62644670 remapped
        to P16086, gi:62664168 remapped to P60711, gi;631898 remapped to P61765,
        gi:62653035 remapped to Q6P9V9,gi:62653090 remapped to Q4FZU2, gi:62654117
        remapped to Q7TP47, gi:70850 remapped to P62909, gi:34876714 remapped to
        B5DEN5, gi:62718633 remapped to P04256, gi:62659231 mapped to Q6URK4, gi:62644588
        also remapped to Q6URK4, gi:62650074 remapped to P62083, gi: 56385</td>
    </tr>
    <tr>
      <td style="text-align:left">EBI-2550901</td>
      <td style="text-align:left">The authors have provided UniProtKB identifiers for most of the proteins.
        Where Ensembl identifiers were provided, mapping to UniProtKB identifiers
        was carried out based on cross-references in UniProtKB, HGNC or MGI records.
        ENSP00000382001 and ENSP00000386061 were mapped to UniProtKB accession
        numbers based on their gene names.</td>
    </tr>
    <tr>
      <td style="text-align:left">EBI-3964609</td>
      <td style="text-align:left">Ensembl protein IDs given in Supplementary Table 1 were mapped to UniProt
        IDs, at the sequence level, using the PICR mapping service.</td>
    </tr>
  </tbody>
</table>### 4.6.7 exp-modification

Experimental details are entered where experiments have a protocol that is non-standard, i.e. where the CV terms for either ‘Interaction Detection’ or ‘Participant Detection’ are not adequate. Example: a modified protocol from the one described in the CV term used.

**Examples**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Accession Number</th>
      <th style="text-align:left">Annotation Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">EBI-6551052</td>
      <td style="text-align:left">Proteins were first coimmunoprecipited with an anti-Flag antibody before
        a second round with the specified bait.</td>
    </tr>
    <tr>
      <td style="text-align:left">EBI-6550960</td>
      <td style="text-align:left">Thymocytes were irradiated (5 Gy) and chromatin was generated either at
        90 minutes later (Fig S4 K/L) or at 0, 30, 60, 90 and 120 minutes later
        (Fig S4 M).</td>
    </tr>
    <tr>
      <td style="text-align:left">EBI-6553615</td>
      <td style="text-align:left">Phoenix cells are a HEK293T variant.</td>
    </tr>
    <tr>
      <td style="text-align:left">EBI-313006</td>
      <td style="text-align:left">
        <p>Binding of purified LRRK1 and LRRK2 to ATP was measured using four different
          ATP derivatives coupled to agarose beads.</p>
        <p>Binding to the beads was inhibited by the addition of free ATP to the
          binding reaction but not GTP.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">EBI-6310657</td>
      <td style="text-align:left">Anti-Flag agarose beads containing 3xFlag-LRRK1 or 3xFlag-LRRK2 were incubated
        with GTP-&#x3B1;-33P alone or with cold nucleotides. After incubation,
        excess nucleotide was removed, and the amount of bound isotopic GTP was
        measured by scintillation counting.</td>
    </tr>
    <tr>
      <td style="text-align:left">EBI-6288136</td>
      <td style="text-align:left">Molecules tagged with a fluorescent label were detected by tag fluorescence.</td>
    </tr>
  </tbody>
</table>### 4.6.8 library-used

This annotation is most frequently used with two hybrid screening assays.

The information about the library which was scanned to obtain the interacting protein clone is recorded under this annotation topic.

Example:

| Experiment AC | Annotation Description |
| :--- | :--- |
| EBI-3925930 | Human liver cDNA library |
| EBI-6502381 | HeLa cDNA library |
| EBI-2298471 | Arabidopsis cDNA library of seedlings subjected to various abiotic stresses as described in the text. |

### 4.6.9 negative

This is used for annotation of experiments that demonstrate that an interaction does not occur, but is used only in very specific circumstances.

#### 4.6.9.1 Rules for annotation of negative interactions.

1. The interaction must have supporting positive interaction data in the same paper before any negative information can be entered.

2. Only experimental data in the same publication or by the same scientific group in another publication that demonstrates the negative interaction is acceptable: do not enter negative interactions based on comments in the paper or ‘data not shown’ since there is no evidence for this shown in the paper.

3. Post-translational modifications inducing negative interaction should be entered as annotation to the positive interactions as this is really supporting evidence for the positive interaction.

4. Protein isoforms that do NOT interact can be entered as negative interactions, provided there is complementary positive interaction data for other isoform/s \(and you must know the exact identity of the isoform that does not interact\).

#### 4.6.9.2 How to make an entry for a negative interaction.

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Positive Experiment</b>
      </th>
      <th style="text-align:left"><b>Negative Experiment</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Experiment - create as usual</td>
      <td style="text-align:left">
        <p>Create a new separate experiment:</p>
        <p>Add the following annotation:</p>
        <p>Annotation topic: negative:</p>
        <p>&apos;This experiment relates to a negative interaction.&#x2019;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Interaction &#x2013; create as usual</td>
      <td style="text-align:left">
        <p>Link negative interaction to positive interaction</p>
        <p>Add the following annotation to the Negative Interaction:</p>
        <p>Annotation topic: negative:</p>
        <p>&#x2018;The interaction does not occur under these experimental conditions.&#x2019;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>To the <b>Positive</b> Expt add an</p>
        <p>X-Ref with Qualifier &#x201C;SEE-ALSO&#x201D;:-</p>
        <p>DataBase = IntAct</p>
        <p>+ Accession Number of the <b>Negative</b> Experiment</p>
      </td>
      <td style="text-align:left">
        <p>To the <b>Negative</b> Expt add an</p>
        <p>X-Ref with Qualifier &#x201C;SEE-ALSO&#x201D;:-</p>
        <p>DataBase = IntAct</p>
        <p>+ Accession Number of the <b>Positive</b> Experiment</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>To the <b>Positive</b> interaction</p>
        <p>Add an X-Ref with Qualifier &#x201C;SEE-ALSO&#x201D;:-</p>
        <p>DataBase =IntAct</p>
        <p>+ accession number of the <b>Negative</b> Interaction</p>
      </td>
      <td style="text-align:left">
        <p>To the <b>Negative</b> Interaction</p>
        <p>Add an X-Ref with Qualifier &#x201C;SEE-ALSO&#x201D;:-</p>
        <p>DataBase =IntAct</p>
        <p>+ accession number of the <b>Positive</b> Interaction</p>
      </td>
    </tr>
  </tbody>
</table>All Negative Reactions can be seen on the Web site by searching in Advanced Fields for “Negative Interaction”.

Note that to see the cross-referenced interactions you will currently have to view the interactions in the Editor.

A few examples:

EBI-6173513, [EBI-4567600](http://www.ebi.ac.uk/intact/interaction/EBI-4567600?conversationContext=2), [EBI-6354102](http://www.ebi.ac.uk/intact/interaction/EBI-6354102?conversationContext=2) - free text comments on the entry

### 4.6.10 uniprot-dr-export

Databases such UniProt, GOA and neXtProt take binary interactions from IntAct and these are selected following a strict set of rules. First, experimental evidences of interaction A-B are merged. Then, the evidences for interaction A-B are then scored, and the interaction exported provided the score crosses a certain threshold, and the molecule pair obeys certain rules, including that the interaction evidences must also include at least one evidence of a binary pair, excluding spoke expanded and colocalisation data, before export.

If a curator is entering two molecules as an effective binary pair e.g. bait and one prey in a coip, but knows from other evidence \(which may be in a separate paper\) that a third ‘bridge’ protein is required for these 2 molecules to interact, the uniprot-dr-export annotation topic can be used to prevent these interactions being used as evidence of a binary pair. Any interaction which should not be used as evidence of a binary pair, should have annotation topic uniprot-dr-export added at the Experiment level, with added annotation text “**no**”. This will probably require the creation of a new Experiment if there are other interactions in the publication where this is not an issue.

Examples:

EBI-6393946: apparent binary pairs according to the limits of this experiment, but the interaction is known to involve other proteins \(so are not true binary interactions\).

EBI-5326135: in the absence of b-catenin the reaction \(of two interactors\) does not occur.

This annotation need only be added if there are only TWO interactors. When there are &gt;2 interactors, the expanded binaries will NOT be exported to UniProt, in the absence of any additional information.

\[This annotation is not to be confused with the “No-UniProt-Update” annotation which is only applied at the participant level, and is added to synthetic protein constructs to stop the Protein Update attempting to map them \(unsuccessfully\) to UniProt.\]

### 4.6.11 variable and variable\_2

These annotations are added to an experiment to describe a set of interaction\(s\) with one/two variable parameters, for example, a kinetic experiment in which the concentration of a substrate or the temperature may be varied, or the effects of increasing concentrations of an agonist may be monitored over time or combinations of any of these.

[EBI-1255485](about:blank) [variable:](about:blank) Time after treatment with 1uM Phorbol 12-myristate 13-acetate \(mins\)

EBI-5237718 variable: Time after Sendai viral infection \(hours\).

EBI-4372312 variable: Insulin \(nM\)

EBI-1570754 variable: The stage of the cell cycle

EBI-4413025 variable: Gamma-irradiation \(Gy\)

Examples of variable data as shown on the Public Web site: \(Dynamic Interactions\)

[http://www.ebi.ac.uk/intact/interaction/EBI-6253708](http://www.ebi.ac.uk/intact/interaction/EBI-6253708)

[http://www.ebi.ac.uk/intact/interaction/EBI-6264089](http://www.ebi.ac.uk/intact/interaction/EBI-6264089)

Other examples with 2 variables:

EBI-1775371 variables: Rapamycin \(ng/ml\) and Insulin \(mM\)

EBI-2620909 variables: Time \(mins\) and IL3 \(ng/ml\)

## 4.7 Experiment cross-references and cross-reference qualifiers

All added cross-references must have a qualifier, which usually needs be added manually.

**Database Qualifier**

pubmed method reference

pubmed see-also

pubmed source reference

intact see-also

### 4.7.1 method

The cross-reference qualifier "method" should be used with database ‘pubmed’ and primary ID the PubMed number, where there is a relevant paper describing the experimental technique used. It should not be used for information about the interactions.

### 4.7.2 see-also

* Used as a qualifier to add additional database links \(e.g. for internally created proteins\) which cannot be added using another qualifier.
* Used to add to entries obtained from an external source such as a database which has an associated publication describing the resource. The PMID should be given the reference qualifier ‘see-also’. Example: [EBI-866743](about:blank).
* Used while referring to an IntAct database cross-reference to an experiment used to show a negative interaction. See section 5.6.9.

### 4.7.3 source reference

This cross-reference is added to entries obtained from an external source such as a database which had an associated publication describing the data. The PMID should be given the reference qualifier ‘source reference’. Example: [EBI-866743](about:blank).

### 4.7.4 target-species

This cross-reference is added automatically and relates to the organism/s of the protein/s involved in the interaction. This cross-reference does not need to be changed by curators.

## 4.8 Data not shown

Normally if an author makes a claim based on ‘Data not shown’ this is not curated. The exception to this is screening data, usually two hybrid or MS proteomics following affinity purification. This may be captured, provided both methodology and results are clearly described in the text.

