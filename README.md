# Rx Almanac Pharma Services Ownership Dataset (2026 snapshot)

Version 2026.1. Snapshot date: 2026-10-04. DOI: https://doi.org/10.5281/zenodo.23137792

**Browse and search the data online:** https://hoytgong.github.io/rxalmanac-ownership-dataset/

**Download:** [`data/rx-almanac-pharma-services-ownership-2026.csv`](data/rx-almanac-pharma-services-ownership-2026.csv) (295 vendors) and [`data/rx-almanac-ownership-events-2024-2026.csv`](data/rx-almanac-ownership-events-2024-2026.csv) (35 events). The same files are archived on Zenodo under the DOI above, which is the version to cite.

This dataset is the structured table behind the Rx Almanac analysis "Who Owns Pharma Services? 2026 Consolidation Findings": https://rxalmanac.com/articles/who-owns-pharma-services-2026/

It records the current publicly disclosed ownership of 295 pharmaceutical services vendors (hub services, specialty pharmacy, copay and patient assistance, market access, commercialization, data and real-world evidence, regulatory, supply chain, and related service lines) and 35 dated ownership events since 2024. The value is the compilation in one table. Every value in the vendor file except `ownership_type` is published on the vendor's public Rx Almanac profile; `ownership_type` is Rx Almanac's classification of that published information. Every event row links to a public announcement or report.

## Files

| File | Rows | What it holds |
|---|---:|---|
| `data/rx-almanac-pharma-services-ownership-2026.csv` | 295 | One row per vendor: identity, website, ownership type, corporate parent, ownership statement, founding year, headquarters |
| `data/rx-almanac-ownership-events-2024-2026.csv` | 35 | One row per acquisition, investment, merger, carve-out, divestiture, or rebrand dated 2024 or later, each with a public source URL |
| `README.md` | | This file |
| `CITATION.cff` | | Citation metadata (GitHub shows a "Cite this repository" button from it) |
| `index.html` | | The searchable online viewer served by GitHub Pages |

Both CSVs are UTF-8 with a header row. Fields containing commas are quoted.

## How the dataset was built

**Vendor universe.** Every vendor with a published profile on rxalmanac.com on the snapshot date. Rx Almanac publishes a profile only for companies that sell to pharmaceutical and biotech manufacturers; companies that serve only payers, providers, or pharmacies are not profiled, so they are not in this table. The directory is curated, not exhaustive. A vendor's absence means it has not been profiled, nothing more.

**Source of each vendor field.** Name and website are taken from the vendor's public profile page at `rxalmanac_url`. Corporate parent, ownership statement, founding year, and headquarters are taken from the Company Details panel on that page. Apart from `ownership_type`, the dataset contains no value that is not shown on the profile on the snapshot date. Rx Almanac maintains those profile facts editorially from company announcements, sponsor and acquirer announcements, regulatory filings, and trade press, and corrects them when a reader supplies a public source.

**Ownership type.** `ownership_type` is Rx Almanac's classification of who controls the vendor. It is maintained editorially for every profile and has been checked against the corporate parent and ownership statement shown on that profile. The classes are:

1. `subsidiary`: a current immediate corporate parent is named on the profile. The parent is the organization that directly owns the operating company. It is usually an operating group. In several rows it is a named holding company: for example the parents recorded for Inizio, Atlantis Health, Envision Pharma Group, GoGoMeds, and AcariaHealth are CD&R Ulysses UK Holdco 2 Limited, Cumulus Business Holding Limited, Evidence Midco Limited, Fortis Holding Company, and Specialty Therapeutic Care Holdings, LLC. Who controls such a holding company is stated in the ownership statement only where the public record establishes it. A sponsor's fund is never recorded as a parent.
2. `pe-backed`: no parent is named and the ownership statement describes the company as private-equity-backed, sponsor-backed, or majority-owned or controlled by a private-equity sponsor.
3. `vc-backed`: no parent is named and the statement describes venture or growth-capital backing without a named private-equity sponsor.
4. `public`: the company itself is listed on a public exchange.
5. `independent-private`: no parent is named and the statement describes a privately held, founder-owned, partner-owned, or employee-owned company. This class also holds companies whose statement names an investor whose stake or control is not publicly established (see Known limits), because the class reflects control, not the presence of an investor.
6. `other`: a structure that fits none of the above (one record: a company owned by its member health systems).

Where a class is a judgment call, the `ownership_statement` column carries the public wording so a reader can judge for themselves.

**Events.** The events file is a transaction ledger kept by Rx Almanac for its Consolidation Atlas. Each row carries one public source URL: a press release, a company or sponsor announcement, a regulatory filing, or trade press. Only events dated 2024 or later and tied to a vendor in the vendor file are included. The `date`, `event_type`, and `event_description` of every row were checked against the cited page on October 3 and 4, 2026 and limited to what that page states; the `target` column may add a short note in parentheses, such as the current Rx Almanac name where a business has since been renamed, or the scope of the asset acquired. It is a count of transaction events, not of unique acquired companies, and it is not a census of all pharma services M&A.

## Field definitions

### rx-almanac-pharma-services-ownership-2026.csv

| Column | Definition |
|---|---|
| `name` | Vendor name as shown on the Rx Almanac profile |
| `slug` | Rx Almanac profile identifier; stable join key to the events file |
| `rxalmanac_url` | Public profile URL, the source page for the row |
| `website` | Vendor's own website as shown on the profile |
| `ownership_type` | One of `pe-backed`, `subsidiary`, `vc-backed`, `independent-private`, `public`, `other` (classes above) |
| `parent_company` | Immediate corporate parent as shown on the profile; blank when none is asserted |
| `ownership_statement` | Public one-line ownership description from the profile |
| `founded` | Founding year as shown on the profile; blank when the profile does not state one |
| `headquarters` | Headquarters city and state or country as shown on the profile; blank when the profile does not state one |
| `snapshot_date` | Date the profile values were captured (2026-10-04) |

### rx-almanac-ownership-events-2024-2026.csv

| Column | Definition |
|---|---|
| `date` | Event date as printed on the cited source page (its dateline or publication date) |
| `target` | Company, business unit, or asset whose ownership changed. For mergers, both parties |
| `acquirer_or_investor` | Acquirer, lead investor, or sponsor. Begins with "None" for a rebrand, a merger with no outside acquirer, or a wind-down |
| `event_type` | One of `lbo`, `take-private`, `growth-equity`, `recapitalization`, `stake-investment`, `acquisition`, `add-on`, `merger`, `carve-out`, `divestiture`, `rebrand` (definitions below) |
| `event_description` | One-line description of the event, limited to what the cited source states |
| `rxalmanac_vendor_slug` | The vendor in the vendor file that the event is recorded against; joins to `slug` |
| `public_source_url` | A public announcement or report of the event |

Event types: `lbo` is a sponsor acquiring or taking a majority of a private company; `take-private` is a sponsor acquiring a listed company; `growth-equity` is a sponsor investment described by the source as a growth or substantial investment without a stated control outcome; `recapitalization` is a change of sponsor or capital structure; `stake-investment` is a strategic or financial investor taking a stake that the source does not describe as control; `acquisition` is one company buying another company outright, whatever the buyer's own ownership; `add-on` is an existing platform company, under any ownership, buying a smaller company or asset to extend its offering; `merger` is two companies combining into one; `carve-out` is a business separated from a larger parent into a standalone company; `divestiture` is a parent exiting a business line; `rebrand` is a name change with no change of control.

## Counts at the snapshot date

| Ownership type | Vendors | Share |
|---|---:|---:|
| subsidiary | 89 | 30.2% |
| independent-private | 69 | 23.4% |
| pe-backed | 67 | 22.7% |
| vc-backed | 47 | 15.9% |
| public | 22 | 7.5% |
| other | 1 | 0.3% |
| Total | 295 | 100% |

Of the 89 subsidiaries, 88 name an immediate corporate parent, and those 88 roll up to 69 parent labels. One subsidiary record (Inmar Rx Solutions) does not assert a parent: its ownership statement says it operates within a privately held group whose immediate legal parent is not established in the public record.

Events since 2024 by type: add-on 10, lbo 6, acquisition 4, growth-equity 3, merger 3, carve-out 2, stake-investment 2, take-private 2, divestiture 1, recapitalization 1, rebrand 1. Total 35.

**Relation to the companion article.** The published article reports figures from a September 16, 2026 snapshot of 286 vendors (61 PE-backed, 86 subsidiaries, 63 private independent, 42 VC-backed, 21 public, 13 unknown). This release is a later snapshot of 295 vendors, so the counts differ by the profiles added in between. Two further differences are deliberate. First, the article carries an "unknown" class; this release has none, because every vendor the internal classification left unresolved has a public ownership statement that states its structure, and the class was assigned from that wording. Second, five vendors are classed here by their public ownership statement where the internal label disagreed with it: Alira Health (vc-backed; the statement says venture-backed), Swoop (pe-backed; the statement names a majority sponsor), Fingerpaint Group (pe-backed; the statement says private equity-backed), Loopback Analytics (independent-private; the statement describes a growth investment with percentages not disclosed), and AscellaHealth (Optime Care) (independent-private; the statement says privately held and no parent is named). The article will be refreshed to this snapshot.

## Known limits

- Snapshot, not a feed. Ownership changes often. Check the vendor's profile at `rxalmanac_url` for the current value.
- 44 vendors have no founding year and 2 have no headquarters on their profile; those cells are blank rather than guessed.
- Parent labels are copied as shown on each profile and are not normalized. The same group can appear under more than one label, for example "Omnicom" and "Omnicom Group", "UPS Healthcare" and "United Parcel Service, Inc.", "Publicis Health" and "Publicis Groupe".
- The `independent-private` class includes 11 companies that name a sponsor, growth investor, or strategic minority holder whose stake or control is not publicly established: Access Infinity, Acumetis, Axtria, Beghou, Blue Matter Consulting, FFF Enterprises, LighthouseAI, Loopback Analytics, LSPedia, Premier Research, and Veristat. The `ownership_statement` says so in each case. In the other direction, SAI MedPartners is classed pe-backed although its statement describes a minority sponsor, AnovoRx is pe-backed with the sponsor's stake size undisclosed, and Senderra Specialty Pharmacy is pe-backed on a majority investment that had regulatory approval but no announced close at the snapshot date.
- Where the cited page reports an agreement or announcement rather than a completed transaction, the `event_description` says "agrees to" or "announces". Closing may have happened after that page was published; the dataset does not assert it.
- The events file records only transactions involving vendors in the vendor file. It is not a complete record of pharma services M&A, and a vendor with no event row has simply had no qualifying event recorded since 2024.
- Six Business Wire releases, two Axios articles, one Fierce Healthcare article, and one Court Square page do not render for automated clients. Those pages were verified through archived copies or a desktop browser on October 3, 2026 and are kept because they are the primary announcements; one Axios Pro article shows only a preview without a subscription.

## How to cite

Rx Almanac (2026). Rx Almanac Pharma Services Ownership Dataset (2026 snapshot), version 2026.1. Zenodo. https://doi.org/10.5281/zenodo.23137792

Please also link to the companion analysis: https://rxalmanac.com/articles/who-owns-pharma-services-2026/

## License

Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0). You may share and adapt the data for non-commercial purposes with attribution to Rx Almanac. For commercial licensing, contact hello@rxalmanac.com.

## Corrections

Factual corrections with a public source are welcome at hello@rxalmanac.com. A correction changes a published value only after it is verified against a source. Corrected values will appear in the vendor's live profile first and in the next dataset version.

## Version history

- 2026.1 (2026-10-04): first public release. 295 vendors, 35 events since 2024.
