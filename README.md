# NeoMundi Signal Adaptation Framework

Cadre conceptuel pour adapter différentes sources de données vers un état normalisé mesurable par NeoMundi.

---

## Objet du dépôt

Ce dépôt décrit le rôle d’une couche d’adaptation entre une source de données et le moteur de mesure NeoMundi.

NeoMundi ne mesure pas directement “du texte”, “une image”, “une vidéo” ou “un marché financier”.

NeoMundi mesure un état normalisé.

Le texte généré par un LLM constitue aujourd’hui le premier cas d’application public. Mais le principe architectural est plus général : toute source capable d’être transformée en représentation d’état normalisée peut, en théorie, être évaluée par le même cadre de mesure.

Ce dépôt ne décrit pas une implémentation complète de normaliseur multimodal. Il définit une frontière conceptuelle, un contrat d’entrée et une direction de recherche.

---

## Principe général

Une source produit un flux.

Ce flux est adapté par une couche dédiée.

Cette couche produit un état canonique.

NeoMundi mesure cet état.

Le résultat est un signal de gouvernance runtime.

```text
Source
  ↓
Signal Adaptation Layer
  ↓
Canonical State
  ↓
NeoMundi Measurement Engine
  ↓
Runtime Governance Signal
```

---

## Pourquoi une couche d’adaptation ?

Les systèmes numériques ne produisent pas tous le même type de sortie.

Un LLM produit du texte.

Un système de vision produit des images, des embeddings, des objets détectés, des trajectoires ou des cartes de confiance.

Un système audio produit des segments temporels, des fréquences, des transcriptions ou des signatures acoustiques.

Un système agentique produit des actions, des appels d’outils, des décisions intermédiaires et des transitions d’état.

Un système financier produit des séries temporelles, des signaux de risque, des flux de prix ou des décisions structurées.

Pour éviter que le moteur NeoMundi dépende d’une seule modalité, une couche d’adaptation permet de convertir ces sorties hétérogènes en représentation d’état comparable, mesurable et interprétable.

Le normaliseur n’est donc pas le produit.

Le produit est la mesure appliquée à un état normalisé.

---

## Séparation des responsabilités

La couche d’adaptation prépare l’état.

Le moteur NeoMundi mesure l’état.

Le système client conserve l’autorité de décision.

Cette séparation est essentielle.

NeoMundi produit des signaux de gouvernance runtime et des artefacts d’audit.

L’autorité de décision reste entre les mains du système client, de la politique configurée ou de l’opérateur responsable.

---

## Contrat conceptuel d’entrée

Une représentation d’état normalisée doit idéalement contenir :

- une unité observable ;
- une fenêtre temporelle ou séquentielle ;
- des variables mesurables ;
- une forme de cohérence interne ;
- une information de variation ;
- une traçabilité minimale ;
- un contexte d’interprétation.

Exemple générique :

```json
{
  "source_type": "llm | vision | audio | multimodal | agent | structured_system",
  "timestamp": "ISO-8601",
  "window_id": "string",
  "state_vector": {},
  "observables": {},
  "context": {},
  "trace": {}
}
```

Ce format n’est pas un standard final. Il sert de base conceptuelle pour penser l’interopérabilité entre sources, adaptateurs et moteur de mesure.

---

## Canonical State

Le Canonical State désigne une représentation intermédiaire permettant à NeoMundi de mesurer un état sans dépendre directement du format natif de la source.

Il ne s’agit pas de reconstruire toute la cognition interne d’un système.

Il ne s’agit pas non plus de prouver la vérité sémantique d’un contenu.

Il s’agit de fournir une représentation suffisamment stable, structurée et observable pour permettre une mesure runtime.

---

## Cas d’application actuel : langage

Dans le cas d’un LLM, la source est une génération textuelle.

La couche d’adaptation peut organiser cette génération en fenêtres observables, par exemple :

```text
tokens
  ↓
runtime windows
  ↓
coherence / stability / variation observables
  ↓
Canonical State
  ↓
NeoMundi Signal
```

Ce cas est le premier domaine public de NeoMundi, car il est directement testable sur les sorties des modèles génératifs actuels.

---

## Extension conceptuelle : vision

Dans un système de vision, la source peut être une image, une séquence vidéo, une carte de segmentation, une détection d’objets ou un embedding visuel.

Une couche d’adaptation dédiée pourrait transformer ces sorties en observables normalisés :

```text
visual input
  ↓
detected structures / embeddings / confidence maps
  ↓
Canonical State
  ↓
NeoMundi Signal
```

Cette extension est conceptuelle à ce stade. Elle ne constitue pas une revendication de disponibilité produit.

---

## Extension conceptuelle : audio

Dans un système audio, la source peut être un signal sonore, une transcription, des segments temporels, des variations de fréquence ou des signatures acoustiques.

Une couche d’adaptation pourrait produire une représentation normalisée de stabilité, de continuité ou de rupture dans le flux audio.

```text
audio stream
  ↓
segments / features / transcription / acoustic observables
  ↓
Canonical State
  ↓
NeoMundi Signal
```

Cette piste est exploratoire.

---

## Extension conceptuelle : systèmes agentiques

Dans un système agentique, la source n’est pas seulement une réponse finale.

Elle peut inclure :

- des appels d’outils ;
- des décisions intermédiaires ;
- des changements de plan ;
- des erreurs de trajectoire ;
- des boucles ;
- des escalades ;
- des transitions entre états.

Une couche d’adaptation agentique pourrait convertir ces transitions en état canonique mesurable.

```text
agent actions
  ↓
tool calls / plans / state transitions
  ↓
Canonical State
  ↓
NeoMundi Signal
```

Ce cas est particulièrement important pour la gouvernance des agents autonomes ou semi-autonomes.

---

## Extension conceptuelle : systèmes financiers ou structurés

Dans un système financier ou décisionnel structuré, la source peut être une série temporelle, un score de risque, une séquence d’ordres, une décision automatisée ou un flux de signaux.

Une couche d’adaptation pourrait représenter ces éléments sous forme d’état séquentiel normalisé.

```text
structured data stream
  ↓
risk variables / time windows / decision states
  ↓
Canonical State
  ↓
NeoMundi Signal
```

Cette extension doit être traitée avec prudence et validation sectorielle spécifique.

---

## Ce que ce dépôt ne revendique pas

Ce dépôt ne revendique pas que NeoMundi mesure déjà toutes les modalités en production.

Il ne revendique pas une preuve universelle de vérité, de sécurité, de conformité ou de causalité.

Il ne revendique pas que la couche d’adaptation remplace l’expertise métier.

Il ne revendique pas qu’un signal NeoMundi constitue à lui seul une autorisation, une certification ou une preuve réglementaire.

Il décrit une architecture d’extension : source, adaptation, état canonique, mesure, signal.

---

## Positionnement scientifique

Le moteur NeoMundi est conçu pour être indépendant de la modalité, à condition qu’une représentation d’état normalisée puisse être produite.

Le texte est le premier cas d’usage public.

Les autres modalités nécessitent des couches d’adaptation dédiées, des protocoles de validation spécifiques et des limites clairement documentées.

Ce dépôt sert à rendre visible cette séparation entre :

- source ;
- adaptation ;
- état canonique ;
- mesure ;
- interprétation ;
- décision.

---

## Formulation courte

NeoMundi ne dépend pas du texte.

NeoMundi dépend d’un état normalisé.

La couche d’adaptation transforme une source hétérogène en état canonique.

Le moteur NeoMundi mesure cet état.

Le système client conserve l’autorité de décision.

---

## Statut

Statut : concept public / cadre exploratoire.

Ce dépôt documente une direction architecturale et méthodologique.

Les implémentations spécifiques par modalité doivent être publiées, testées et validées séparément.
