# <a name="class-mipcontentlabel"></a>Classe mip::ContentLabel 
Astrazione per un'etichetta di Microsoft Information Protection applicata a un contenuto, in genere un documento.
Oltre alle informazioni sull'etichetta, contiene le proprietà per una specifica etichetta applicata.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string & GetCreationTime | Ottiene l'ora di creazione dell'etichetta.
public AssignmentMethod GetAssignmentMethod | Ottiene il metodo di assegnazione dell'etichetta.
public std::shared_ptr< Label > GetLabel | Ottiene l'effettivo oggetto etichetta applicato al contenuto.
## <a name="members"></a>Membri
### <a name="getcreationtime"></a>GetCreationTime
Ottiene l'ora di creazione dell'etichetta.
#### <a name="returns"></a>Returns
Ora di creazione sotto forma di stringa GMT.
### <a name="getassignmentmethod"></a>GetAssignmentMethod
Ottiene il metodo di assegnazione dell'etichetta.
#### <a name="returns"></a>Returns
AssignmentMethod STANDARD, PRIVILEGED, AUTO. 
**Vedere anche**: mip::AssignmentMethod
### <a name="label"></a>Label
Ottiene l'effettivo oggetto etichetta applicato al contenuto.
#### <a name="returns"></a>Returns
Oggetto etichetta applicato al contenuto. 
**Vedere anche**: [mip::Label](#classmip_1_1_label)