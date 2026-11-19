# Lager-Chatbot (RAG)

Ein kleiner Chatbot, der Fragen zu Lager-Arbeitsanweisungen beantwortet.
Er antwortet **nur** anhand der hinterlegten Dokumente und sagt ehrlich,
wenn die Antwort nicht drinsteht.

## So funktioniert es

1. **Retrieval (Suche):** Die Frage wird in Wortanfänge zerlegt und mit den
   Textstücken (Chunks) der Arbeitsanweisungen verglichen. Jeder Treffer
   bekommt Punkte.
2. **Schwelle:** Ist der beste Treffer zu schwach, wird Claude gar nicht
   aufgerufen. Das verhindert falsche Antworten und spart Kosten.
3. **Generation (Antwort):** Die besten Treffer gehen an die Claude-API.
   Claude formuliert eine kurze Antwort und nennt die Quelle.

## Beispiel

| Frage | Ergebnis |
|---|---|
| Was muss ich vor jeder Schicht am Stapler prüfen? | Gabeln, Bremsen, Hupe (stapler.txt) |
| Wie hoch darf ich entzündbare Stoffe stapeln? | Maximal 2 Paletten (gefahrgut.txt) |
| Wer ist der Bundeskanzler? | Dazu habe ich nichts in den Unterlagen gefunden. |

## Bekannte Grenze

Die Stichwortsuche versteht keine Synonyme. Die Frage „Wie schnell darf man
fahren?“ findet den Satz mit „Höchstgeschwindigkeit“ nicht, weil die Wörter
keine gemeinsamen Anfangsbuchstaben haben.

## Nächste Schritte

- Suche mit Embeddings statt Stichwörtern (findet Bedeutung statt Buchstaben)
- Dokumente direkt aus Textdateien einlesen
- Eingabefeld statt fest eingebauter Testfragen

## Technik

Python, Google Colab, Anthropic Claude API. Der API-Key liegt als
Colab-Secret `ANTHROPIC_API_KEY` und steht nicht im Code.

Alle Dokumente im Projekt sind erfundene Beispiele.
