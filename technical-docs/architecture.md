---
title: Architektur
parent: Technical Docs
nav_order: 1
layout: home
---

{: .label }

{: .no_toc }

# Architektur

> Diese Seite beschreibt, wie die Anwendung strukturiert ist und wie wichtige Teile der App funktionieren. Sie soll neuen Teammitgliedern ausreichend technisches Wissen vermitteln, um zum Code beizutragen.

<details open markdown="block">
{: .text-delta }
<summary>Inhaltsverzeichnis</summary>
+ ToC
{: toc }
</details>

### Überblick

# Frontend:

## HTML-Templates:

Definieren die Struktur und den Inhalt der Webseiten und ermöglichen die Darstellung dynamischer Daten.

## Bootstrap:

Ein Framework für responsive und moderne Weblayouts mit vordefinierten CSS-Klassen und JavaScript-Komponenten. Es erleichtert die schnelle Erstellung ansprechender und konsistenter Benutzeroberflächen.

## Flask WTForms (Formulargenerierung und -validierung im Frontend):

Erstellung und Validierung von HTML-Formularen im Browser. Es bietet eine bequeme Möglichkeit, Formulare zu generieren und zu validieren, bevor sie an den Server gesendet werden.

## Jinja-Templates:

Ermöglichen die dynamische Generierung von HTML durch Einbettung von Python-Code. Jinja-Templates bieten eine flexible Möglichkeit, Inhalte und Layouts zu gestalten und Daten aus dem Backend an das Frontend zu übergeben.

# Backend:

## Flask (Routing und HTTP-Anfragen-Verarbeitung):

Verwaltet Routen und verarbeitet HTTP-Anfragen. Es ermöglicht die Definition von Endpunkten und die Verarbeitung eingehender Anfragen.

## Python (Geschäftslogik):

Implementierung der Kernfunktionalität der Anwendung. Python wird verwendet, um die Logik zu schreiben, die die App antreibt.

## Flask WTForms (Formularvalidierung im Backend):

Serverseitige Validierung der Formulardaten. Stellt sicher, dass die Daten korrekt und sicher sind, bevor sie verarbeitet oder in die Datenbank gespeichert werden.
