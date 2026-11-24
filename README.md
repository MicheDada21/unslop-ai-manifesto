# unslop-ai-manifesto

Sottrae lo slop da un repository, dal codice morto ai workaround alle istruzioni per agenti superate, in piccoli lotti che non cambiano il comportamento, poi aggiunge controlli automatici.

Fa parte della [Prompt Library di CH Labs](https://www.cryptohelvetia.com/ch-labs/prompt-library). Il repo contiene una copia della skill, rigenerata a ogni aggiornamento della libreria.

## Installare

In Claude Code aggiungi una volta il marketplace e installa il plugin.

```
/plugin marketplace add MicheDada21/ch-labs-skills
/plugin install unslop-ai-manifesto@ch-labs-skills
```

Da shell i comandi sono `claude plugin marketplace add MicheDada21/ch-labs-skills` e `claude plugin install unslop-ai-manifesto@ch-labs-skills`. Nell'app desktop premi + accanto al campo del prompt, apri Plugins, aggiungi il marketplace `MicheDada21/ch-labs-skills` con Add marketplace e poi il plugin con Add plugin.

Con altri agenti copia la cartella `skills/unslop-ai-manifesto` tra le skill dell'agente, per esempio in `~/.codex/skills/unslop-ai-manifesto`.

## Licenza

MIT, testo completo in [LICENSE](LICENSE).
