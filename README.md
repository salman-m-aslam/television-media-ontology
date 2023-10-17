# television-media-ontology

Infer new relationships between entities in the television media domain using a semantic network.

### Execution instructions:
- Open tvshows.ipynb (Jupyter notebook) in Google Colab.
- Place tvshows.dtd (DTD), tvshows.owl (ontology), tvshows.xml (XML) and other/tvshowsInferences.owl (empty ontology to save inferences into) in the working directory.
- Execute all the code blocks within the .ipynb file.
- In case of any issue during multiple runs, restart the runtime and run all the code blocks again.

### Results:
- tvshowsUpdatedWithXMLData.owl (Extracted triples)
- tvshowsInferences.owl (Inferred triples)

### Steps:
1. Design a television media ontology (TBox) using the description logic SROIQ
2. Design a DTD to structure television media data and create an instance of the it
3. Model the ontology using OWL in Protege
4. Combine the television media data with the ontology and infer triples using the HermiT reasoner

### DTD Design:
1. Containment was made relatively low for reuse of an element, without repetition of the entire element, simple by referring to it using its ID.
2. Certain elements were created exclusively to refer to other elements.
3. A product may be a result of a brand collaboration. Therefore, multiple brand references are allowed within a product element.
4. Middle name was made optional as all people don't have have it.
5. Since an address could have multiple data items, an addressline element was created to represent them.
6. A person could have multiple names in different contexts.
7. An actor was modelled as someone who has played at least one character.
8. Separate sub elements for currency and value were created for the price element for ease of parsing this data.
9. Area code of a phone number also had its own element for easier parsing.
10. The telecast element is used to denote the shows in a particular channel slot.
11. Subcategory of a product was made optional since certain categories would be too specific to have meaningful subcategories.

### Ontology Design and Dev.:
1. Even though ‘Address’ was modelled as a class, ‘addressLine’ was modelled as a property. This is simpler to use.
2. A new 'adAgencyCreator' property was created to connect an 'Advertisement' to 'adAgency'.
3. 'subClassOf' was used to make anonymous classes and set restrictions to classes like stating that a 'Character' should have one or more 'Name'.
4. 'Show' telecasted in a 'Slot' was modelled using a property 'telecastedShow'.
5. A 'Person' was modelled as a 'Thing' that could be an 'Actor' (real) or a 'Character' (imaginary).
6. 'MediaPlatform' was designed as the disjoint union of 'OTTPlatform' and 'TVChannel'. There are other such cases too.
7. A new 'ProductType' class was created to denote 'Category and 'Subcategory' of a 'Product'.
8. 'Show' telecasted in a 'Slot' was modelled using a property 'telecastedShow'.
9. As is the usual case, some inverse properties were named, like actsAs (actedBy) with domain and range being specified only for one of them.
10. As multiple 'ContactInfo' could be associated with a 'Person', each instance of it was modelled to be stating either only emails or only phone numbers.
11. Some instances were added to the ontology for testing during design itself.

### Inference Using Reasoner:
1. In the final part, a program was created to extract the television media data from the earlier created xml dtd instance and combine it with the earlier created ontology
2. Triples were added to the ontology using properties like owns, ownedBy, etc.
3. Additional triples were inferred
