---
# NOTE: This file is auto-generated from 'scripts/error-docgen.mjs'
# Do not make edits to it directly, they will be overwritten.
# Instead, change this file: https://github.com/withastro/astro/blob/main/packages/astro/src/core/errors/errors-data.ts
# Translators, please remove this note and the <DontEditWarning/> component.

layout: ~/layouts/MainLayout.astro
title: Astro.clientAddress is not available in current adapter.
i18nReady: true
githubURL: https://github.com/withastro/astro/blob/main/packages/astro/src/core/errors/errors-data.ts
setup: |
  import DontEditWarning from '../../../../components/DontEditWarning.astro';
---

<DontEditWarning />


> **ClientAddressNotAvailable**: `Astro.clientAddress` is not available in the `ADAPTER_NAME` adapter. File an issue with the adapter to add support. (E03002)

## What went wrong?
The adapter you.'re using unfortunately does not support `Astro.clientAddress`.

**See Also:**
-  [Official integrations](/en/guides/integrations-guide/#official-integrations)
-  [Astro.clientAddress](/en/reference/api-reference/#astroclientaddress)


