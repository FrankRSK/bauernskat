Benennung der MP3-Dateien

Damit das neue System funktioniert, musst du deine MP3-Dateien in deinem sounds-Ordner nach einem bestimmten Muster benennen:

    Für Sound-Typen mit Variationen hängst du einen Unterstrich und eine Zahl an. Wenn du zum Beispiel für cardPlay in der Konfiguration 5 eingetragen hast, erwartet das Skript Dateien mit den Namen:

        cardPlay_1.mp3

        cardPlay_2.mp3

        cardPlay_3.mp3

        cardPlay_4.mp3

        cardPlay_5.mp3

    Für Sound-Typen ohne Variationen (oder wenn du in der Konfiguration 1 einträgst), bleibt der Dateiname wie bisher:

        trump.mp3

        playerSelectsTrump.mp3

Jetzt wird bei jedem Aufruf von playSound('cardPlay') zufällig eine der fünf hinterlegten MP3s abgespielt. Das sorgt für eine tolle, abwechslungsreiche Geräuschkulisse!

Anleitung zur Benennung der neuen Sound-Dateien

Damit die geschlechtsspezifischen Sounds funktionieren, musst du deine Dateinamen im sounds-Ordner wie folgt anpassen:

    Für KI-Aktionen: Hänge an den Sound-Typ das Geschlecht (_male oder _female) an.

        Beispiel (männlich): computerWinsTrick_male.mp3

        Beispiel (weiblich): computerWinsTrick_female.mp3

    Für KI-Aktionen mit Variationen: Hänge zusätzlich die Variationsnummer an.

        Beispiel (männlich): computerWinsTrick_male_1.mp3, computerWinsTrick_male_2.mp3

        Beispiel (weiblich): computerWinsTrick_female_1.mp3, computerWinsTrick_female_2.mp3

    Für die Trumpffarben: Lege einfach eine MP3-Datei mit dem Namen der Farbe an.

        Beispiele: Herz.mp3, Pik.mp3, Karo.mp3, Kreuz.mp3, Grand.mp3
