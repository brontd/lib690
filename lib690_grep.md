*Learning Grep

`````
Scopus
EXPORT DATE: 17 February 2024

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
`````

grep -o 'author = {.*[a-z]' scopus.bib | cut -d"{" -f2
