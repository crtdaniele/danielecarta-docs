---
id: redux
title: Redux
---

## Cos'è Redux?

Redux è una architettura per gestire lo stato in applicazioni web basate ad esempio su React. Il suo scopo è quello di rendere prevedibile il cambio di stato tramite l’imposizione di alcune restrizioni su come e quando questo può avvenire.

### 3 fondamenti di Redux

1. Lo stato è archiviato in un unico archivio (quindi ci sarà un unico oggetto javascript che conterrà lo store).
2. Lo stato è di sola lettura è può esser cambiato solo tramite le action di Redux
3. Lo stato viene cambiato dai reducer che sono delle funzioni pure

### Action

Sono dei semplici oggetti JS che definiscono il tipo di azione che dovrà andare a fare poi il reducer, prendono come proprietà generalmente chiamata type.