# Lager-Chatbot (RAG)

Ein kleiner Chatbot, der Fragen zu Lager-Arbeitsanweisungen beantwortet.
Er antwortet **nur** anhand der hinterlegten Dokumente und sagt ehrlich,
wenn die Antwort nicht drinsteht.

## So funktioniert es

1. **Dokumente:** Die Arbeitsanweisungen liegen als `.txt`-Dateien im Ordner
   `unterlagen`. Jede Zeile wird ein Textstück (Chunk). Neue Dateien werden
   beim Start automatisch eingelesen.
2. **Retrieval (Suche):** Frage und Textstücke werden mit einem
   Embedding-Modell (sentence-transformers) in Zahlenvektoren umgewandelt.
   Die Suche findet die Textstücke mit der größten Bedeutungsähnlichkeit,
   auch wenn andere Wörter benutzt werden. Pro Textstück wird das Thema
   (Dateiname) mit eingebettet, das verbessert die Treffer deutlich.
3. **Schwelle:** Liegt der beste Treffer unter einem Ähnlichkeitswert
   (0.35), wird Claude gar nicht aufgerufen. Das verhindert falsche
   Antworten und spart Kosten.
4. **Generation (Antwort):** Die drei besten Treffer gehen an die Claude-API.
   Claude formuliert eine kurze Antwort und nennt die Quelle.

## Beispiel

| Frage | Ergebnis |
|---|---|
| Wo lagere ich Gefahrgut? | Im gekennzeichneten Bereich C (gefahrgut.txt) |
| Wie schnell darf der Stapler fahren? | 10 km/h (verkehr.txt) |
| Wie lange darf ich Mittagspause machen? | 30 Minuten (pausen.txt) |
| Wer ist der Bundeskanzler? | Dazu habe ich nichts in den Unterlagen gefunden. |

## Entwicklung in zwei Versionen

- **Version 1:** Stichwortsuche. Sie fand Synonyme nicht, z. B. wurde
  „schnell“ nicht mit „Höchstgeschwindigkeit“ verbunden.
- **Version 2:** Suche mit Embeddings. Das Problem ist gelöst. Außerdem
  wurde die Schwelle an echten Testfragen eingestellt und das Thema in die
  Suche aufgenommen.

## Bekannte Grenzen

- Die Schwelle (0.35) ist an wenigen Testfragen eingestellt. Mit mehr
  Dokumenten muss sie neu geprüft werden.
- Jede Zeile einer Textdatei wird ein Textstück. Längere Absätze werden
  nicht automatisch sinnvoll aufgeteilt (Chunking).

## Nächste Schritte

- Längere Texte sinnvoll in Abschnitte zerlegen (Chunking)
- Mehr Testfragen, um die Schwelle besser einzustellen
- Einfache Oberfläche statt Eingabe im Notebook

## Technik

Python, sentence-transformers, Google Colab, Anthropic Claude API.
Der API-Key liegt als Colab-Secret `ANTHROPIC_API_KEY` und steht nicht im Code.

Alle Dokumente im Projekt sind erfundene Beispiele.
