# Diagramme d'activité - Blanchisserie Tourbillon

```mermaid
flowchart LR
  %% Swimlanes
  subgraph Client
    CL1["Demande de ramassage"]
    CL2["Remise du linge - ramassage"]
    CL3["Reception linge propre"]
  end

  subgraph Administration et Planification - Sebastien
    AD1["Saisie unique de la demande"]
    AD2["Planifier tournees et production"]
    AD3["Emettre ordres de mission et de production"]
    AD4["Cloture BL et facturation"]
  end

  subgraph Maintenance et Logistique - Fabien
    MA1["Verifier disponibilite machines et vehicules"]
    MA2["Traiter incident machine"]
    MA3["Remettre en service et maj statut"]
  end

  subgraph Production
    PR1["Reception -2 / pesee / scan"]
    PR2["Tri initial"]
    PR3["Traitement froid si contamine"]
    PR4["Lavage"]
    PR5["Sechage / finition / QC"]
    PR6["Conditionnement"]
    PR7["Expedition / livraison"]
  end

  %% Flux principal
  CL1 --> AD1 --> AD2 --> AD3 --> PR1
  CL2 --> PR1
  PR1 --> PR2
  PR2 -- "contamine" --> PR3 --> PR4
  PR2 -- "non contamine" --> PR4
  PR4 --> PR5 --> PR6 --> PR7 --> CL3
  PR7 --> AD4

  %% Interactions maintenance (pointilles)
  AD2 -. "disponibilite" .-> MA1
  PR4 -. "panne" .-> MA2 -.-> MA3 -. "OK reprise" .-> PR4
