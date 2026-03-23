# 🎯 Nutzen und Funktionsweise
Dieses kleine Skript/Bookmarklet ermöglicht es, eine veröffentlichte Prio-Liste von der Seite https://sahne-team.de per Klick direkt im CSV-Format auszugeben, welches z.B. für den Import in das Addon "Prio 3" benötigt wird. So muss keine Datei mehr lokal gespeichert und geöffnet werden.

# 🔧 Einrichtung
## 1. 📜 Code in die Zwischenablage kopieren:
> javascript:(()=>{const root=document.getElementById('tabausgeben');if(!root){alert('Kein Element mit ID "tabausgeben" gefunden.');return;}const table=root.querySelector('table');if(!table){alert('Keine Tabelle in #tabausgeben gefunden.');return;}const rows=[...table.querySelectorAll('tr[id]')].filter(tr=>tr.closest('table')===table);const csv=rows.map(tr=>{const nameCell=tr.cells[1];const nameNode=nameCell?nameCell.cloneNode(true):document.createElement('td');[...nameNode.querySelectorAll('img')].forEach(img=>img.remove());const name=nameNode.textContent.replace(/\s+/g,' ').trim();const itemIds=[...tr.querySelectorAll('[data-wowhead*="item="]')].map(el=>{const m=(el.getAttribute('data-wowhead')||'').match(/(?:^|[&;])item=(\d+)/);return m?m[1]:null;}).filter(Boolean);return [name,...itemIds].join(';');}).filter(Boolean).join('\n');alert(csv||'Keine passenden Zeilen gefunden.');})();

## 2. 🗃️ Neues Lesezeichen im Browser erstellen
- Name/Titel: Beliebig (z.B. "Sahne Prio Export")
- URL: Hier den Code aus der Zwischenablage einfügen.
- 
## 3. 📤 Liste exportieren
Wenn das Bookarklet auf angeklickt wird, während eine öffentliche Sahne-Prio-Liste zu sehen ist, wird die Liste im CSV-Format direkt im Browser angezeigt und kann kopiert werden.

## 4. 📥 Liste importieren
Im Addon "Prio 3" kann dieser CSV-Export nun eingefügt werden.
