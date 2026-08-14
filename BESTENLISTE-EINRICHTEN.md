# Schweizer Bestenliste einrichten

Die Liste "🇨🇭 SCHWEIZ" braucht eine Datenbank, die alle Spieler erreichen.
Das Spiel selbst liegt auf GitHub Pages und kann nichts speichern.

Wir nutzen **Supabase** (kostenlos, keine Kreditkarte). Dauert ca. 5 Minuten.

## 1. Projekt anlegen

1. Auf <https://supabase.com> ein Konto anlegen und einloggen.
2. **New project** anklicken, Name z.B. `racerx`, Region Europa (Frankfurt),
   ein Datenbank-Passwort setzen (brauchst du hier nicht mehr) und erstellen.
3. Warten, bis das Projekt bereit ist.

## 2. Tabelle anlegen

Links im Menü **SQL Editor** öffnen, das hier einfügen und auf **Run** klicken:

```sql
create table results (
  id      bigint generated always as identity primary key,
  name    text not null,
  team    text,
  track   text,
  pos     int,
  time    text,
  best    text,
  best_ms bigint,
  ts      bigint
);

-- Zugriffsregeln: jeder darf Ergebnisse lesen und eigene eintragen,
-- aber niemand darf etwas aendern oder loeschen.
alter table results enable row level security;

create policy "alle duerfen lesen"
  on results for select using (true);

create policy "alle duerfen eintragen"
  on results for insert with check (true);
```

## 3. Schlüssel ins Spiel eintragen

1. Links **Project Settings → API** öffnen.
2. Dort stehen **Project URL** und der Key **anon public**.
3. In `index.html` den Block `const WORLD` suchen (ziemlich weit oben im Script)
   und beides eintragen:

```js
const WORLD={
  url:'https://deinprojekt.supabase.co',
  key:'eyJhbGciOi...',        // der anon public Key
  table:'results'
};
```

Der `anon public` Key darf öffentlich im Code stehen — genau dafür ist er da.
Den `service_role` Key **niemals** eintragen, der darf alles.

## 4. Hochladen

```bash
git add index.html
git commit -m "Bestenliste aktiviert"
git push
```

Nach ein paar Minuten ist es auf <https://mikkel-thiemann.github.io/MikkelRacer/>
aktiv. Ab dann landet jedes beendete Rennen in der gemeinsamen Liste.

## Gut zu wissen

- In der Bestenliste steht **der Name des Fahrers** statt des Teams. Der Name ist
  der, den man am Anfang eingibt — also für alle sichtbar. Am besten keinen
  echten Nachnamen verwenden.
- Gezeigt wird pro Fahrer und Strecke nur die **schnellste Runde**,
  sortiert von schnell nach langsam. Deine eigene Zeile ist gelb.
- Der Streckenfilter funktioniert auch in der Bestenliste.
- Jeder kann Eintraege schicken, auch mit erfundenen Zeiten — es gibt keine
  Pruefung. Fuer ein Spiel unter Freunden ist das ok.
- Falls jemand Unsinn eintraegt: im Supabase **Table Editor** die Zeile
  einfach loeschen.
- Das kostenlose Kontingent (500 MB) reicht fuer Millionen von Rennen.
