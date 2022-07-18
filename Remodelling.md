### Remodelling GAM_Users_interactions

```
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX arco: <https://w3id.org/arco/ontology/arco/> 
PREFIX xyz: <http://sparql.xyz/facade-x/data/> 
PREFIX arco-cp: <https://w3id.org/arco/ontology/context-description/> 
PREFIX arco-dd: <https://w3id.org/arco/ontology/denotative-description/> 
PREFIX arco-core: <https://w3id.org/arco/ontology/core/> 
PREFIX cis: <http://dati.beniculturali.it/cis/> 
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> 
PREFIX dc: <http://purl.org/dc/elements/1.1/> 
PREFIX scripting: <https://w3id.org/spice/SON/scripting/> 
PREFIX l0: <https://w3id.org/italia/onto/l0/>
PREFIX emotion: <https://w3id.org/spice/SON/emotion/>
PREFIX vcvf: <http://www.ontologydesignpatterns.org/ont/values/valuecore_with_value_frames.owl#>

CONSTRUCT {
  ?artworkIRI a arco:CulturalProperty .
  ?artworkIRI owl:sameAs ?cp .
  ?artworkIRI arco-cp:title ?title .
  ?artworkIRI cis:identifier ?identifier .
  ?artworkIRI arco-cp:subject ?subjectIRI .
  ?artworkIRI arco-cp:hasAuthorshipAttribution ?authorshipIRI .
  ?authorshipIRI arco-cp:hasAttributedAuthor ?authorIRI .
  ?authorIRI rdfs:label ?author . 
  ?subjectIRI rdfs:label ?subject .
  ?artworkIRI arco-cp:isMemberOfCollectionOf ?collectionMembershipIRI .
  ?collectionMembershipIRI a arco-cp:CollectionMembership .
  ?collectionMembershipIRI arco-cp:hasMemberOfCollection ?artworkIRI .
  ?collectionMembershipIRI arco-cp:hasCollection ?collectionIRI .
  ?collectionIRI a l0:Collection .
  ?collectionIRI arco-cp:title ?collectionName .
  ?artworkIRI arco-cp:hasDating ?datingIRI . 
  ?datingIRI a arco-cp:Dating . 
  ?datingIRI rdfs:label ?year .
  ?artworkIRI arco-dd:hasMaterialOrTechnique ?technique . 
  ?technique a arco-dd:TechnicalCharacteristic . 
  ?technique rdfs:label ?mt .
  ?artworkIRI arco-dd:hasMeasurement ?measurementIRI . 
  ?measurementIRI a arco-dd:Measurement . 
  ?measurementIRI rdfs:label ?measurementLabel . 
  ?artworkIRI arco-core:description ?definition ; arco-core:description ?dc_description .
  ?artworkIRI arco-cp:hasAcquisition ?acquisitionIRI .
  ?acquisitionIRI rdfs:comment ?acquisition .
  ?artworkIRI arco-cp:depiction ?image .
  ?artworkIRI emotion:triggers ?emotionIRI .
  ?artworkIRI vcvf:triggers ?valueIRI .
  
  ?userIRI a scripting:Agent .
  
  ?interactionThinkAboutIRI scripting:involves ?artworkIRI .
  ?interactionThinkAboutIRI a scripting:InteractionWithCulturalProperty .
  ?interactionOfUserThinkAboutIRI scripting:executesTask ?interactionThinkAboutIRI .
  ?interactionOfUserThinkAboutIRI scripting:generated ?think_about_reification .
  ?think_about_reification rdfs:label ?think_about .
  
  ?interactionMakesMeFeelIRI scripting:involves ?artworkIRI .
  ?interactionMakesMeFeelIRI a scripting:InteractionWithCulturalProperty .
  ?interactionOfUserMakesMeFeelIRI scripting:executesTask ?interactionMakesMeFeelIRI .
  ?interactionOfUserMakesMeFeelIRI scripting:generated ?makes_me_feel_reification .
  ?makes_me_feel_reification rdfs:label ?makes_me_feel .
  
} WHERE { 
  ?cp <http://sparql.xyz/facade-x/data/%40id> ?cpId .
  BIND(IRI(CONCAT("https://w3id.org/spice/Artwork/GAM_",?cpId)) AS ?artworkIRI) 
  
  ?cp xyz:title ?title .
  ?cp xyz:collection ?collectionName .
  BIND(IRI(CONCAT("https://w3id.org/spice/Collection/GAM_Collection_", ENCODE_FOR_URI(?collectionName))) AS ?collectionIRI)
  BIND(IRI(CONCAT("https://w3id.org/spice/Collection/GAM_CollectionMembership_",?cpId,"_", ENCODE_FOR_URI(?collectionName))) AS ?collectionMembershipIRI)
  
  ?cp xyz:inventary ?identifier .
  BIND(IRI(CONCAT("https://w3id.org/spice/GAM/GAM_Subject_", ENCODE_FOR_URI(?subject))) AS ?subjectIRI)
  
  ?cp xyz:subject ?subject .
  ?cp xyz:author ?author .
  BIND(IRI(CONCAT("https://w3id.org/spice/GAM/", ENCODE_FOR_URI(?author))) AS ?authorIRI)
  BIND(IRI(CONCAT("https://w3id.org/spice/GAM/Authorship_attribution_",?cpId,"_", ENCODE_FOR_URI(?author))) AS ?authorshipIRI)
  
  ?cp xyz:year ?year .
  BIND(IRI(CONCAT("https://w3id.org/spice/GAM/GAM_",?cpId,"_dating")) AS ?datingIRI) 
  
  ?cp xyz:materialAndTechnique ?mt .
  BIND(IRI(CONCAT("https://w3id.org/spice/GAM/MaterialAndTechnique_",ENCODE_FOR_URI(?mt))) AS ?technique)
  
  ?cp xyz:dimention ?measurementLabel .
  BIND(IRI(CONCAT("https://w3id.org/spice/GAM/GAM_",?cpId,"_measurement")) AS ?measurementIRI)
  
  ?cp xyz:definition ?definition .
  
  ?cp <http://sparql.xyz/facade-x/data/dc%3Asource> ?acquisition .
  BIND(IRI(CONCAT("https://w3id.org/spice/GAM/GAM_",?cpId,"_acquisition")) AS ?acquisitionIRI)
  
  ?cp xyz:image ?image . 
  ?cp <http://sparql.xyz/facade-x/data/dc%3Adescription> ?dc_description .
  
  ?cp xyz:degari_extracted_emotions ?emotion_array .
  ?emotion_array ?slot ?emotion .
  BIND(IRI(CONCAT("https://w3id.org/spice/SON/PlutchikEmotion/",ENCODE_FOR_URI(?emotion))) AS ?emotionIRI) 
  
  ?cp xyz:degari_extracted_values ?value_array .
  ?value_array ?slotval ?value .
  BIND(IRI(CONCAT("https://w3id.org/spice/SON/Value/",ENCODE_FOR_URI(?value))) AS ?valueIRI) 

  ?cp xyz:unito_users ?users .
  ?users ?user_id ?user .
  BIND(IRI(CONCAT("https://w3id.org/spice/GAM/User_",?user_id)) AS ?userIRI)
  
  ?user xyz:think_about ?think_about .
  BIND(IRI(CONCAT("https://w3id.org/spice/GAM/InteractionThinkAbout_", ?cpId)) AS ?interactionThinkAboutIRI) 
  BIND(IRI(CONCAT("https://w3id.org/spice/GAM/InteractionThinkAbout_of_",?user_id,"_with_", ?cpId)) AS ?interactionOfUserThinkAboutIRI)
  BIND(IRI(CONCAT("https://w3id.org/spice/GAM/Think_about_reification_",ENCODE_FOR_URI(?think_about))) AS ?think_about_reification) 
  
  ?user xyz:makes_me_feel ?makes_me_feel .
  BIND(IRI(CONCAT("https://w3id.org/spice/GAM/InteractionMakesMeFeel_", ?cpId)) AS ?interactionMakesMeFeelIRI) 
  BIND(IRI(CONCAT("https://w3id.org/spice/GAM/InteractionMakesMeFeel_of_",?user_id,"_with_", ?cpId)) AS ?interactionOfUserMakesMeFeelIRI)   
  BIND(IRI(CONCAT("https://w3id.org/spice/GAM/MakesMeFeel_reification_",ENCODE_FOR_URI(?makes_me_feel))) AS ?makes_me_feel_reification) 
  
} LIMIT 1
```
