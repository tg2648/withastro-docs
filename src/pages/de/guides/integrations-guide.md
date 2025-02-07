---
layout: ~/layouts/MainLayout.astro
title: Integrationen nutzen
i18nReady: true
setup: |
  import IntegrationsNav from '~/components/IntegrationsNav.astro';
  import PackageManagerTabs from '~/components/tabs/PackageManagerTabs.astro'
---

**Astro-Integrationen** ermöglichen es dir, mit nur wenigen Zeilen Code neue Funktionen und Verhaltensweisen zu deinem Projekt hinzuzufügen. Du kannst eine Integration selbst schreiben, eine offizielle Integration verwenden oder Integrationen aus der Community nutzen.

Integrationen können…

- React, Vue, Svelte, Solid und andere beliebte UI-Frameworks nutzbar machen.
- Tools wie Tailwind und Partytown mit wenigen Zeilen Code integrieren.
- Neue Features zu deinem Projekt hinzufügen, wie z.B. automatische Sitemap-Generierung.
- Eigenen Code schreiben, der sich in den Erzeugungsprozess, den Entwicklungs-Server und mehr einhängen lässt.

## Offizielle Integrationen

<IntegrationsNav />

## Automatische Einrichtung von Integrationen

Astro stellt ein `astro add`-Kommando zur Verfügung, um die Einrichtung von Integrationen zu automatisieren.

:::caution
Wir werden immer um Bestätigung bitten, bevor wir deine Dateien aktualisieren. Jedoch ist es empfehlenswert, ein Versionskontroll-Backup zu haben.
:::

Führe das `astro add`-Kommando mit dem Paketmanager deiner Wahl aus, und unser automatischer Integrations-Wizard wird deine Konfigurationsdatei aktualisieren und alle notwendigen Abhängigkeiten installieren.

<PackageManagerTabs>
  <Fragment slot="npm">
  ```shell
  npx astro add react
  ```
  </Fragment>
  <Fragment slot="pnpm">
  ```shell
  pnpx astro add react
  ```
  </Fragment>
  <Fragment slot="yarn">
  ```shell
  yarn astro add react
  ```
  </Fragment>
</PackageManagerTabs>

Es ist sogar möglich, mehrere Integrationen gleichzeitig zu konfigurieren!

<PackageManagerTabs>
  <Fragment slot="npm">
  ```shell
  npx astro add react tailwind partytown
  ```
  </Fragment>
  <Fragment slot="pnpm">
  ```shell
  pnpx astro add react tailwind partytown
  ```
  </Fragment>
  <Fragment slot="yarn">
  ```shell
  yarn astro add react tailwind partytown
  ```
  </Fragment>
</PackageManagerTabs>

:::note[Behandlung von Abhängigkeiten deiner Integrationen]
Solltest du eine Warnung wie `Cannot find package '[package-name]'` nach dem Hinzufügen einer Integration erhalten, hat dein Paketmanager vermutlich nicht die zugehörigen [Peer Dependencies](https://nodejs.org/en/blog/npm/peer-dependencies/) installiert. Um diese fehlenden Abhängigkeiten zu installieren, führe einfach `npm install [package-name]` aus.
:::

## Integrationen nutzen

Astro-Integrationen werden immer über die `integrations`-Option in deiner `astro.config.mjs`-Datei konfiguriert.

Es gibt drei übliche Wege, um eine Integration in dein Astro-Projekt zu importieren:
1. Eine Integration über ein npm-Paket installieren.
2. Deine eigene Integration über eine lokale Datei innerhalb deines Projekts importieren. 
3. Deine eigene Integration direkt in der Konfigurationsdatei schreiben.

```js
// astro.config.mjs
import {defineConfig} from 'astro/config';
import installedIntegration from '@astrojs/vue';
import localIntegration from './my-integration.js';

export default defineConfig({
  integrations: [
    // 1. Aus einem installiertem npm-Paket importieren
    installedIntegration(),
    // 2. Aus einer lokalen JS-Datei importieren
    localIntegration(),
    // 3. Ein Inline-Objekt
    {name: 'namespace:id', hooks: { /* ... */ }},
  ]
})
```

Sieh dir die [Integrations-API](/de/reference/integrations-reference/) an, um mehr darüber zu erfahren, wie du deine eigenen Integrationen erstellen kannst.

### Benutzerdefinierte Optionen

Integrationen werden in der Regel als Factory-Funktionen entwickelt, die das Integrations-Objekt zurückliefern. Dadurch kannst du Argumente und Optionen an die Funktion übergeben, um die Integration zu konfigurieren.

```js
integrations: [
  // Beispiel: Argumente an eine Integration übergeben
  sitemap({filter: true})
]
```

### Integrationen aktivieren und deaktivieren

Integrationen mit `falsy`-Werten werden ignoriert. Dadurch können sie aktiviert oder deaktiviert werden, und man muss sich keine Gedanken über hinterlassene `undefined`- und Boolean-Werte machen.

```js
integrations: [
  // Beispiel: Keine Sitemap unter Windows erstellen
  process.platform !== 'win32' && sitemap()
]
```

## Weitere Integrationen entdecken

Eine Vielzahl von Integrationen, die durch die Community entwickelt werden, können in [Astros Integrations-Verzeichnis](https://astro.build/integrations/) gefunden werden. Folge den dortigen Links, um detaillierte Anleitungen zu ihrer Benutzung und Konfiguration zu erhalten.

## Eine eigene Integration erstellen

Astros Integrations-API ist durch Rollup und Vite inspiriert und wurde so gestaltet, dass sie sich für alle vertraut anfühlen sollte, die jemals ein Rollup- oder Vite-Plugin geschrieben haben.

Sieh dir die [Integrations-API](/de/reference/integrations-reference/) an, um mehr darüber zu erfahren, was Integrationen leisten können und wie du deine eigenen Integrationen erstellen kannst.
