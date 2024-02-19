# Learning Grep

## Sample File Snippet

Scopus
EXPORT DATE: 17 February 2024

```
@ARTICLE{Adams2023100,
        author = {Adams, Harrison},
        title = {Vija Celmins: The Art of Enervation},
        year = {2023},
        journal = {Zeitschrift fur Kunstgeschichte},
        volume = {86},
        number = {1},
        pages = {100 – 127},
        doi = {10.1515/ZKG-2023-1007},
        url = {https://www.scopus.com/inward/record.uri?e
        abstract = {The painter Vija Celmins has long bee
        author_keywords = {entropy; Jorge Luis Borges; ma
        correspondence_address = {H. Adams; email: harrya
        publisher = {Deutscher Kunstverlag GmbH},
        issn = {00442992},
        language = {English},
        abbrev_source_title = {Z. Kunstgesch.},
        type = {Article},
        publication_stage = {Final},
        source = {Scopus},
        note = {Cited by: 0; All Open Access, Hybrid Gold
}

@ARTICLE{Petriceks2023,
        author = {Petriceks, Aldis H.},
        title = {Irrevocably other: Narrative medicine an
        year = {2023},
        journal = {Palliative and Supportive Care},
        doi = {10.1017/S1478951523000895},
        url = {https://www.scopus.com/inward/record.uri?e
        affiliations = {Harvard Medical School, Boston, M
        correspondence_address = {A.H. Petriceks; Harvard
        publisher = {Cambridge University Press},
        issn = {14789515},
        language = {English},
        abbrev_source_title = {Palliative Supportive Care
        type = {Editorial},
        publication_stage = {Article in press},
        source = {Scopus},
        note = {Cited by: 0; All Open Access, Bronze Open
}
```

Pull author using grep piped to cut

```
grep -o 'author = {.*[a-z]' scopus.bib | cut -d"{" -f2
```

Results in:

```
Adams, Harrison
Petriceks, Aldis
García, Patricia
Cara, Ana
Pfennig, Isabel Serra
Joy, Dhanya and James, Siby
Surendralal, Sumithra
Otis, Laura
Phungula, Njabulo
Galván-Díaz, Félix Joaquín
Martinson
Kristal, Efraín
Law, Andrew
```

Pull date by piping grep to secondary grep

```
grep -i 'year' scopus.bib | grep -Po '\d{4}'
```

Results in:

```
2023
2023
2023
```

Experimenting with Lookarounds to pull data from between braces, e.g.:

```
title = {Vija Celmins: The Art of Enervation} ==> Vija Celmins: The Art of Enervation
```
 
In other (perhaps more sophisticated) regex implementations, searches can employ parentheses to capture matches that can then be designated as replacement strings.
Thus,

```
title = {the title}" might be matched by (pseudo-code) /^\t title = {(.?)}/
```

wherein the match, in this case, defined by `(.?)` would be held in `$1` variable (subsequent matches in `$2`, `$3`, etc.). Since grep doesn't appear to support this (as far as I can determine), the lookaround functionality offers a viable, grep-only, answer.

```
grep -oiP "(?<=\ttitle = {).*((?=}))" scopus.bib
```

Results in:

```
Vija Celmins: The Art of Enervation
Irrevocably other: Narrative medicine and Jorge Luis Borges' "The other death"
AESTHETIC MODES OF THE INFINITE: HORROR, SUBLIMITY, AND RELATIONALITY
On the High Art of Folk Poetry: What Jorge Luis Borges and Bob Dylan Have in Common
HILDE SPIEL AND GISÈLE FREUND AND THE EXPERIENCE OF EXILE. TESTIMONIES AND DOCUMENTS OF AN AGE; [HILDE SPIEL I GISÈLE FREUND I L'EXPERIÈNCIA DE L'EXILI. TESTIMONIS I DOCUMENTS D'UNA ÈPOCA]; [HILDE SPIEL Y GISÈLE FREUND Y LA EXPERIENCIA DEL EXILIO. TESTIMONIOS Y DOCUMENTOS DE UNA ÉPOCA]
Mirrored Zoontologies: Animalia in the Works of Jorge Luis Borges
Fiction and Philosophy of Science: Paired Readings for the Science Classroom
Creative Writing: Embracing Unfamiliar Knowledge
Sonic labyrinths: form and creative process in like knotted strings (2022) for string quartet
Fiction in Pain: Mourning and Melancholia in Borges's Emma Zunz and El Aleph; [Ficción en el dolor: duelo y melancolía en Emma Zunz y El Aleph de Borges]
Reflexivity’s Ontological Turn: From Cybernetics to Autopoiesis in “The Circular Ruins” and The People of Paper
Jorge Luis Borges’s Theory and Practice of Translation
Incompatibilism and the garden of forking paths
```
