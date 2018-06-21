# <a name="class-mipuserrights"></a>Classe mip::UserRights 
Rappresenta un gruppo di utenti e i diritti ad essi associati.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public UserRights(const UserList& users, const RightList& rights)  |  Costruttore [UserRights](class_mip_userrights.md).
 public const UserList& Users() const  |  Ottiene gli utenti associati a un set di diritti.
 public const RightList& Rights() const  |  Ottiene i diritti associati a un gruppo di utenti.
  
## <a name="members"></a>Membri
  
### <a name="userrights"></a>UserRights
Costruttore [UserRights](class_mip_userrights.md).

Parametri:  
* **users**: gruppo di utenti che condividono gli stessi diritti 


* **rights**: diritti condivisi dal gruppo di utenti


  
### <a name="userlist"></a>UserList
Ottiene gli utenti associati a un set di diritti.

  
**Restituisce**: utenti associati a un set di diritti
  
### <a name="rightlist"></a>RightList
Ottiene i diritti associati a un gruppo di utenti.

  
**Restituisce**: diritti associati a un gruppo di utenti