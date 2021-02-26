# How to specify curated mutations for [outbreak.info Situation Reports](https://outbreak.info/situation-reports)

## Required fields
- `mutation_name`: name of the report
- `reportType`: `"lineage"` || `"mutation"` || `"Lineage + Mutation"`
- `reportQuery`: parameters to route the actual Mutation Report page in Vue. `pango` or `muts` is required, rest is optional.
  - `pango`: string containing PANGO lineage
  - `muts`: array of strings of the mutations. Should be in the form: `{gene}:{ref_aa}{codon_num}{alt_aa}`, e.g. `S:N501Y`. Case sensititive
  - `country`: (optional) array of countries to display in the curated report
  - `division`: (optional) array of divsions to display in the curated report
  - `selected`: (optional) string of the place which is selected by default. Ideally, should be the first place the mutation(s) was detected.
  - `selectedType`: (optional) if `selected` is used, should indicate if `selected` is a `"country"` or `"division"`
  
## Recommended fields
- `mutations`: array contianing the characteristic mutations
  - `mutation`: mutation string name
  - `type`: `"substitution"`, `"deletion"`, or `"insertion"`
  - `gene`: gene
  - `ref_aa`: original amino acid at that position
  - `codon`: codon number of the amino acid, relative to the start of the geen
  - `alt_aa`: mutated amino acid at that position
  - `cahnge_lnegth_nt`: (required for deletions) length of the deletion in nucleotides
  - `ref_codon`: (optional) original nucleotide at that position 
  - `pos`: (optional) absolute nucleotide coordinates of the mutation, relative to the reference sequence
- `variantType`: `"Variant of Concern"` or `"Variant of Interest"` for Lineage or Lineage + Mutation Reports.
- `nextstrain_clade`: Nextstrain Clade
- `mutation_synonyms`: array containing synonyms for the lineage or mutation
- `searchTerms`: Array of strings contianing serach terms to lookup in [Outbreak Resources](https://outbreak.info/resources)
 
## Optional fields
- `description`: Customizable intro text to the Mutation Report
- `disclaimer`: Customizable warnings for why the data are unreliable.

## Example

```
  "mutation_name": "B.1.1.7 + S:E484K",
    "reportType": "Lineage + Mutation",
    "reportQuery": {
      "pango": "B.1.1.7",
      "muts": ["S:E484K"],
      "country": ["United Kingdom", "United States"],
      "division": ["California"],
      "selected": "United Kingdom",
      "selectedType": "country"
    },
    "nextstrain_clade": "20I/501Y.V1",
    "mutation_synonyms": ["Variant of Concern 202012/01", "VOC-202012/01", "20B/501Y.V1", "20I/501Y.V1"],
    "searchTerms": ["B.1.1.7", "Variant of Concern 202012/01", "VOC-202012/01", "202012/01", "20B/501Y.V1", "20I/501Y.V1", "501Y.V1", "voc 20201201", "voc-202012/01", "vui 20201201"],
    "variantType": "Variant of Concern",
    "location_first_identified": "United Kingdom",
    "description": "Concerns surrounding a new strain of SARS-CoV-2 (hCov-19), the virus behind the COVID-19 pandemic, have been developing. <b>B.1.1.7 lineage</b>, also known as <span class='text-highlight'>Variant of Concern 202012/01</span> (VOC-202012/01) or <span class='text-highlight'>20B/501Y.V1</span>, was first identified in the UK in September 2020 and has since been detected in the US and other countries. This is of growing concern because it has shown to be significantly more transmissible than other variants.",
    "disclaimer": "B.1.1.7 genomes in the US were identified by S-gene target failures (SGTF) in community-based diagnostic PCR testing. Since this is not an unbiased approach, it does not indicate the true prevalence of the B117 lineage.  <a class='text-light text-underline ml-3' href='https://outbreak.info/situation-reports/caveats'>How to interpret this report</a>",
    "mutations": [{
      "mutation": "ORF1a:T1001I",
      "type": "substitution",
      "gene": "ORF1a",
      "ref_codon": "ACT",
      "pos": 3266,
      "ref_aa": "T",
      "codon_num": 1001,
      "alt_aa": "I"
    } ...
]
```
