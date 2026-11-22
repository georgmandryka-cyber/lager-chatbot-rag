# Lager-Chatbot (RAG)

Ein kleiner Chatbot, der Fragen zu Lager-Arbeitsanweisungen beantwortet.
Er antwortet **nur** anhand der hinterlegten Dokumente und sagt ehrlich,
wenn die Antwort nicht drinsteht.

## So funktioniert es

1. **Retrieval (Suche):** Frage und Textstücke (Chunks) werden mit einem
   Embedding-Modell (sentence-transformers) in Zahlenvektoren umgewandelt.
   Die Suche findet die Chunks mit der größten Bedeutungsähnlichkeit,
   auch wenn andere Wörter benutzt werden.
2. **Schwelle:** Liegt der beste Treffer unter einem Ähnlichkeitswert
   (0.3), wird Claude gar nicht aufgerufen. Das verhindert falsche
   Antworten und spart Kosten.
3. **Generation (Antwort):** Die besten Treffer gehen an die Claude-API.
   Claude formuliert eine kurze Antwort und nennt die Quelle.

## Beispiel

| Frage | Ergebnis |
|---|---|
| Was muss ich vor jeder Schicht am Stapler prüfen? | Gabeln, Bremsen, Hupe (stapler.txt) |
| Wie hoch darf ich entzündbare Stoffe stapeln? | Maximal 2 Paletten (gefahrgut.txt) |
| Wer ist der Bundeskanzler? | Dazu habe ich nichts in den Unterlagen gefunden. |

## Bekannte Grenzen

- Die Schwelle (0.3) ist an wenigen Testfragen eingestellt. Mit mehr
  Dokumenten muss sie neu geprüft werden.
- Die Dokumente stehen fest im Code und werden nicht aus Dateien gelesen.

## Nächste Schritte

- Dokumente direkt aus Textdateien einlesen
- Eingabefeld statt fest eingebauter Testfragen
- Mehr Testfragen, um die Schwelle besser einzustellen

## Technik

Python, sentence-transformers, Google Colab, Anthropic Claude API. Der API-Key liegt als Colab-Secret `ANTHROPIC_API_KEY` und steht nicht im Code.

Alle Dokumente im Projekt sind erfundene Beispiele.
