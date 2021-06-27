# Grafowa Baza Danych 2021  
  
### Opis projektu oraz wykorzystane źródła  
  
1. Opis  
  
Celem projektu było stworzenie bazy danych chorób wraz z symptomami, lekami stosowanymi przy leczeniu, możliwymi działaniami zapobiegającymi zachorowaniu oraz możliwych podejmowanych akcjach przy danej chorobie.  
  
2. Źródła  
  
Przy tworzeniu bazy zostały wykorzystane pliki z danymi w formacie CSV.    
  
Pliki „Symptom-severity.csv”, „dataset.csv”, „Symptom_Description.csv”, „symptom_precaution.csv” pochodzą ze strony:  
https://www.kaggle.com/itachi9604/disease-symptom-description-dataset.    
Zostały one zmodyfikowane i przystosowane do utworzenia bazy.  
  
Dane zebrane w pliku „disease_medications.csv” pochodzą ze strony https://www.drugs.com.  
  
Informacje z pliku „disease_prevention .csv” zebrane zostały ze stron:  
https://www.cdc.gov,  
https://www.healthline.com,  
https://www.nhs.uk,  
https://my.clevelandclinic.org/health.  
  
### Węzły i właściwości  
  
• Disease – zawiera informacje o nazwie choroby oraz jej opis  
• Medication – zawiera informacje o nazwie leku, jego interakcji z alkoholem oraz czy jest na receptę, czy nie  
• Symptom – zawiera informacje o nazwie symptomu oraz jego wadze (wartości od 1-7)  
• Precaution – zawiera opis akcji podejmowanych po zachorowaniu  
• Prevention – zawiera informacje o nazwie oraz opisie zachowań zapobiegających zachorowaniu  
  
Liczba węzłów: 334  
  
### Relacje  
  
• (Disease) - [can_be_prevented_with] -> (Prevention)  
• (Disease) - [can_be_treated_with] -> (Medication)  
• (Disease) - [can_cause] -> (Symptom)  
• (Medication) - [can_help_with] -> (Disease)  
• (Precaution) - [can_inhibit] -> (Disease)  
• (Symptom) - [can_mean] -> (Disease)  
• (Prevention) - [can_prevent] -> (Disease)  
  
Liczba relacji: 922  
  
### Przykładowe zapytania  
  
MATCH (n) RETURN n  
  
MATCH p=()-[r:can_inhibit]->() RETURN p  
  
MATCH (a)<-[:can_cause]-(b)-[:can_be_treated_with]->(c) RETURN a,b,c  
  
MATCH (a)<-[:can_cause]-(b)-[:can_be_treated_with]->(c) WHERE b.name ="Chicken pox" RETURN a,b,c  
  
MATCH (a)<-[:can_cause]-(b)-[:can_be_treated_with]->(c), (d)-[:can_inhibit]->(b)-[:can_be_preveneted_with]->(e) WHERE b.name = "Common Cold" RETURN a,b,c,d,e  
  
MATCH (n:Symptom) RETURN n ORDER BY n.weight DESC  
