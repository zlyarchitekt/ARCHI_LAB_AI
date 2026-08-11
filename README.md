# ARCHI_LAB_AI — manifest wyłącznika

Ten plik steruje działaniem wtyczki **GIS_ARCHICAD**.

`wylacznik.json` jest **podpisany kluczem Ed25519**. Jest publiczny i tak ma być —
nie zawiera nic tajnego. Liczy się autentyczność, nie poufność: bez klucza prywatnego
nikt nie podrobi treści, więc podmiana pliku czy przekierowanie domeny nic nie da.

## Jak wyłączyć wtyczkę

W repozytorium `GIS_ARCHICAD`:

```powershell
python tools\podpisz_manifest.py --wylacz
```

potem wgraj powstały `wylacznik.json` tutaj (gałąź `main`). Wtyczka przestanie
pobierać dane najpóźniej po 24 godzinach, a u osób uruchamiających ArchiCAD
na nowo — od razu.

Żeby włączyć z powrotem: to samo bez `--wylacz`.

## Pola

| pole | znaczenie |
|---|---|
| `wylaczone` | `true` = wtyczka odmawia pobierania danych |
| `wersjaMin` | wersje starsze niż podana przestają działać |
| `komunikat` | dodatkowy tekst pokazany użytkownikowi (opcjonalny) |
| `wystawiono` | znacznik czasu podpisu |

**Klucz prywatny nie znajduje się w żadnym repozytorium.** Jego utrata oznacza brak
możliwości zmiany manifestu — trzymaj kopię zapasową.
