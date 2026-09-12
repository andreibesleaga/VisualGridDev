# Licence for Normative Artefacts

This repository is **dual-licensed by artefact type**.

## 1. Prose, narrative, and illustration — CC BY-NC-ND 4.0

Essays, descriptive architecture narrative, capability prose, README files,
UI mockups, and images are licensed under
[Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International](LICENSE)
(CC BY-NC-ND 4.0).

## 2. Normative artefacts — Apache License 2.0

The following artefacts are **normative** and are licensed under the
[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0). A copy of
the licence text is included in this repository at [LICENSE-APACHE](LICENSE-APACHE),
as Apache-2.0 section 4(a) requires:

- Protocol and interface schemas, including `Architecture/Schemas/**`.
- Conformance requirements and requirement keywords, including
  [CONFORMANCE.md](CONFORMANCE.md).
- Requirement identifiers and their statements.
- Diagram sources in PlantUML or other machine-readable form, where they define
  normative structure.

### Apache License 2.0 notice

```text
Copyright 2025-2026 Andrei Nicolae Besleaga

Licensed under the Apache License, Version 2.0 (the "License");
you may not use these normative artefacts except in compliance with the
License. You may obtain a copy of the License at

    https://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

## Why the split exists

CC BY-NC-ND 4.0 is a content licence. Its _NoDerivatives_ term prohibits
distributing a modified version of the material, and its _NonCommercial_ term
prohibits commercial use. A normative specification whose purpose is to drive
conforming implementations cannot carry those terms: an implementer must be able
to build, extend, and republish conforming work, and a vendor must be able to
ship a compliant product.

This is the same split used by mature specification bodies. W3C, IETF, OASIS,
and the OpenAPI Initiative each license normative specification text permissively
while reserving separate terms for prose and branding.

## Scope limits

- No licence here grants rights in third-party standards, protocol names,
  trademarks, data, logos, screenshots, or referenced works. See the licences of
  those works.
- No licence here grants any right to operate safety-critical, industrial, or
  regulated systems.
- The non-commercial restriction in CC BY-NC-ND 4.0 continues to apply to the
  prose and illustration categories.

## Contribution

By contributing a normative artefact you agree that it is licensed under
Apache-2.0, and by contributing prose you agree that it is licensed under
CC BY-NC-ND 4.0. See [CONTRIBUTING.md](CONTRIBUTING.md).
