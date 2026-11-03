# nf-core/references-datasheets: agents

## Path placeholders

Pipelines resolve placeholders in datasheet values with nf-schema `validation.allowParamsSubstitution`.

- Only one placeholder is allowed: `${params.references_base_path}`. Do not add other `${params.*}` placeholders.
- `${params.references_base_path}` replaces the bucket root of every path in the datasheet, quoted:
  - `igenomes/`: `s3://ngi-igenomes/igenomes` -> `"${params.references_base_path}/..."`
  - `genomes/`: `s3://nf-core-references` -> `"${params.references_base_path}/..."`
- A pipeline run sets a single `references_base_path`, so a datasheet must not mix files from different roots (for example `s3://ngi-igenomes` and `s3://nf-core-references`). Split it into separate datasheets instead.
- Paths outside these roots (`https://raw.githubusercontent.com/...`, `s3://nf-core-references-scratch/...`) stay absolute.
- `genomes_source/` datasheets keep absolute source URLs: they are inputs to nf-core/references, not read by pipelines.
