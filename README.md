# Miscellaneous

```python
prompt = f"""
    You are a professional academic information extraction expert. Please extract head entities (head entities) from the following text as comprehensively as possible. Each document should extract 30-40 entities.

# Extraction Requirements
1. Head entities are the starting nodes in the knowledge graph's triple (Head Entity, Relation, Tail Entity), representing the entities that initiate the relationship or act as the subject of the relationship. For example:
   - In the triple "Apple Inc. - Founded in - 1976", "Apple Inc." is the head entity.
   - In "Beijing - Is - Capital of China", "Beijing" is the head entity.
2. Each entity must include all applicable type labels (multiple selections are possible).
3. Extract entities of the following types:
   - (Identifier)
   - (Structure/Composition)
   - (Action)
   - (Value)
   - (Function)
   - (Applicability/Context)

# Example (Do not include this example in actual extraction)
{
    "document": "sample.md",
    "entities": [
        {
            "index": 1,
            "entity": "ITU-T G.652 fiber",
            "type": ["Identifier", "Structure/Composition", "Applicability/Context"],
            "context": "ITU-T G.652 fiber was originally optimized for the 1310 nm wavelength region but can also be used in the 1550 nm region.",
            "confidence": 0.92,
        },
        {
            "index": 2,
            "entity": "Wavelength Division Multiplexing (WDM) technology",
            "type": ["Action", "Function"],
            "context": "Wavelength Division Multiplexing (WDM) technology can significantly increase the transmission capacity of optical fibers.",
            "confidence": 0.88,
        }
    ]
}

# Special Notes
1. Do not omit any entities that may meet the criteria in the text.
2. Label each entity with as many applicable types as possible (usually 2-3 types).
3. For long documents, ensure that the number of extractions reaches 30-40.
4. Head entities are the basic units of a knowledge graph, connecting to tail entities through relationships to form a knowledge network. For example: (Head Entity: Apple Inc.) → (Relationship: Headquarters) → (Tail Entity: Cupertino)

# Text to be analyzed (from document: {pdf_name})
{text[:MAX_TOKENS * 4]}  # Increase text truncation length

# Please return the results strictly in the following JSON format:
{
    "document": "File Name",
    "entities": [
        {
            "index": Index,
            "entity": "Entity Name",
            "type": ["Type 1", "Type 2", ...],  # Must use list format
            "context": "Context of Appearance",
            "confidence": Confidence (0-1),
        }
    ],
    "extraction_stats": {
        "total_entities": Total number of entities,
        "coverage_estimate": "Document coverage estimate"
    }
}
"""
